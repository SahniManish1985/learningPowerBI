---
layout: api
title: visualEvents
description: Custom Visuals Rendering Events API
group: references
toc: true
github_issue_id: 467
---

The new API have three methods (started, finished or failed) to be called during performing the rendering.

When rendering starts, the custom visual code calls the renderingStarted method to indicate that rendering process has started.

If the rendering was completed successfully, the custom visual code will immediately call the renderingFinished method notifying the listeners (primarily 'export to PDF' and 'export to PowerPoint') that the visual's image is ready.

In case a problem occurred during the rendering process, preventing the custom visual to successfully complete, the custom visual code should call the renderingFailed method notifying the listener that the rendering process has not completed and also will be providing an optional string for the cause of failure.

#### Methods

| Method&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Return type | Brief description |
|---|---|---|
| renderingStarted(options: VisualUpdateOptions) | void | Should be called just before the actual rendering has started. Usually at the very start of the update method. |
| renderingFinished(options: VisualUpdateOptions) | void | Should be called immediately after successfully completing rendering. |
| renderingFailed(options: VisualUpdateOptions, reason?: string) | void | Called when rendering has failed with an optional reason return string. |

#### Sample
 
```typescript
    export class Visual implements IVisual {
        ...
        private events: IVisualEventService ;
        ...

        constructor(options: VisualConstructorOptions) {
            ...
            this.events = options.host.eventService;
            ...
        }

        public update(options: VisualUpdateOptions) {
            this.events.renderingStarted(options);
            ...
            this.events.renderingFinished(options);
        }
```
