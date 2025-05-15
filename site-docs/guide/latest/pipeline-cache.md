# Pipeline Cache

## Metadata

- **Component**: guide
- **Version**: latest
- **URL**: /guide/latest/pipeline_cache.html

## Content

Pipeline caching is a technique used with VkPipelineCache objects to reuse pipelines that have already been created. Pipeline creation can be somewhat costly - it has to compile the shaders at creation time for example. The big advantage of a pipeline cache is that the pipeline state can be saved to a file to be used between runs of an application, eliminating some of the costly parts of creation. There is a great Khronos presentation on pipeline caching from SIGGRAPH 2016 (video) starting on slide 140. While pipeline caches are an important tool, it is important to create a robust system for them which Arseny Kapoulkine talks about in his blog post. To illustrate the performance gain and see a reference implementation of pipeline caches Khronos offers a sample and tutorial.
