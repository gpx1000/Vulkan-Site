# Image Operations

## Metadata

- **Component**: spec
- **Version**: latest
- **URL**: /spec/latest/chapters/textures.html

## Table of Contents

- [Image Operations Overview](#_image_operations_overview)
- [Image_Operations_Overview](#_image_operations_overview)
- [Texel Coordinate Systems](#textures-texel-coordinate-systems)
- [Texel_Coordinate_Systems](#textures-texel-coordinate-systems)
- [Conversion Formulas](#_conversion_formulas)
- [RGB to Shared Exponent Conversion](#textures-RGB-sexp)
- [RGB_to_Shared_Exponent_Conversion](#textures-RGB-sexp)
- [Shared Exponent to RGB](#textures-sexp-RGB)
- [Shared_Exponent_to_RGB](#textures-sexp-RGB)
- [Texel Input Operations](#textures-input)
- [Texel_Input_Operations](#textures-input)
- [Texel Input Validation Operations](#textures-input-validation)
- [Texel_Input_Validation_Operations](#textures-input-validation)
- [Instruction/Sampler/Image View Validation](#textures-operation-validation)
- [Instruction/Sampler/Image_View_Validation](#textures-operation-validation)
- [Integer Texel Coordinate Validation](#textures-integer-coordinate-validation)
- [Integer_Texel_Coordinate_Validation](#textures-integer-coordinate-validation)
- [Cube Map Edge Handling](#textures-cubemapedge)
- [Cube_Map_Edge_Handling](#textures-cubemapedge)
- [Sparse Validation](#textures-sparse-validation)
- [Layout Validation](#textures-layout-validation)
- [Format Conversion](#textures-format-conversion)
- [Texel Replacement](#textures-texel-replacement)
- [Depth Compare Operation](#textures-depth-compare-operation)
- [Depth_Compare_Operation](#textures-depth-compare-operation)
- [Conversion to RGBA](#textures-conversion-to-rgba)
- [Conversion_to_RGBA](#textures-conversion-to-rgba)
- [Component Swizzle](#textures-component-swizzle)
- [Sparse Residency](#textures-sparse-residency)
- [Chroma Reconstruction](#textures-chroma-reconstruction)
- [Explicit Reconstruction](#textures-explicit-reconstruction)
- [Implicit Reconstruction](#textures-implict-reconstruction)
- [Sampler Y′CBCR Conversion](#textures-sampler-YCbCr-conversion)
- [Sampler_Y′CBCR_Conversion](#textures-sampler-YCbCr-conversion)
- [Sampler Y′CBCR Range Expansion](#textures-sampler-YCbCr-conversion-rangeexpand)
- [Sampler_Y′CBCR_Range_Expansion](#textures-sampler-YCbCr-conversion-rangeexpand)
- [Sampler Y′CBCR Model Conversion](#textures-sampler-YCbCr-conversion-modelconversion)
- [Sampler_Y′CBCR_Model_Conversion](#textures-sampler-YCbCr-conversion-modelconversion)
- [Texel Output Operations](#_texel_output_operations)
- [Texel_Output_Operations](#_texel_output_operations)
- [Texel Output Validation Operations](#textures-output-validation)
- [Texel_Output_Validation_Operations](#textures-output-validation)
- [Texel Format Validation](#textures-format-validation)
- [Texel_Format_Validation](#textures-format-validation)
- [Texel Type Validation](#textures-type-validation)
- [Texel_Type_Validation](#textures-type-validation)
- [Integer Texel Coordinate Validation](#textures-output-coordinate-validation)
- [Integer_Texel_Coordinate_Validation](#textures-output-coordinate-validation)
- [Sparse Texel Operation](#textures-output-sparse-validation)
- [Sparse_Texel_Operation](#textures-output-sparse-validation)
- [Texel Output Format Conversion](#textures-output-format-conversion)
- [Texel_Output_Format_Conversion](#textures-output-format-conversion)
- [Normalized Texel Coordinate Operations](#textures-normalized-operations)
- [Normalized_Texel_Coordinate_Operations](#textures-normalized-operations)
- [Projection Operation](#textures-projection)
- [Derivative Image Operations](#textures-derivative-image-operations)
- [Derivative_Image_Operations](#textures-derivative-image-operations)
- [Cube Map Face Selection and Transformations](#_cube_map_face_selection_and_transformations)
- [Cube_Map_Face_Selection_and_Transformations](#_cube_map_face_selection_and_transformations)
- [Cube Map Face Selection](#_cube_map_face_selection)
- [Cube_Map_Face_Selection](#_cube_map_face_selection)
- [Cube Map Coordinate Transformation](#textures-cube-map-coordinate-transform)
- [Cube_Map_Coordinate_Transformation](#textures-cube-map-coordinate-transform)
- [Cube Map Derivative Transformation](#_cube_map_derivative_transformation)
- [Cube_Map_Derivative_Transformation](#_cube_map_derivative_transformation)
- [Scale Factor Operation, LOD Operation and Image Level(s) Selection](#textures-lod-and-scale-factor)
- [Scale_Factor_Operation,_LOD_Operation_and_Image_Level(s)_Selection](#textures-lod-and-scale-factor)
- [Scale Factor Operation](#textures-scale-factor)
- [Scale_Factor_Operation](#textures-scale-factor)
- [LOD Operation](#textures-level-of-detail-operation)
- [Image Level(s) Selection](#textures-image-level-selection)
- [Image_Level(s)_Selection](#textures-image-level-selection)
- [(s,t,r,q,a) to (u,v,w,a) Transformation](#textures-normalized-to-unnormalized)
- [(s,t,r,q,a)_to_(u,v,w,a)_Transformation](#textures-normalized-to-unnormalized)
- [Unnormalized Texel Coordinate Operations](#_unnormalized_texel_coordinate_operations)
- [Unnormalized_Texel_Coordinate_Operations](#_unnormalized_texel_coordinate_operations)
- [(u,v,w,a) to (i,j,k,l,n) Transformation and Array Layer Selection](#textures-unnormalized-to-integer)
- [(u,v,w,a)_to_(i,j,k,l,n)_Transformation_and_Array_Layer_Selection](#textures-unnormalized-to-integer)
- [Integer Texel Coordinate Operations](#textures-integer-coordinate-operations)
- [Integer_Texel_Coordinate_Operations](#textures-integer-coordinate-operations)
- [Image Sample Operations](#textures-sample-operations)
- [Image_Sample_Operations](#textures-sample-operations)
- [Wrapping Operation](#textures-wrapping-operation)
- [Texel Gathering](#textures-gather)
- [Texel Filtering](#textures-texel-filtering)
- [Texel Nearest Filtering](#textures-texel-nearest-filtering)
- [Texel_Nearest_Filtering](#textures-texel-nearest-filtering)
- [Texel Linear Filtering](#textures-texel-linear-filtering)
- [Texel_Linear_Filtering](#textures-texel-linear-filtering)
- [Texel Cubic Filtering](#textures-texel-cubic-filtering)
- [Texel_Cubic_Filtering](#textures-texel-cubic-filtering)
- [Texel Range Clamp](#textures-texel-range-clamp)
- [Texel_Range_Clamp](#textures-texel-range-clamp)
- [Texel Mipmap Filtering](#textures-texel-mipmap-filtering)
- [Texel_Mipmap_Filtering](#textures-texel-mipmap-filtering)
- [Texel Anisotropic Filtering](#textures-texel-anisotropic-filtering)
- [Texel_Anisotropic_Filtering](#textures-texel-anisotropic-filtering)
- [Texel Footprint Evaluation](#textures-footprint)
- [Texel_Footprint_Evaluation](#textures-footprint)
- [Weight Image Sampling](#textures-weightimage)
- [Weight_Image_Sampling](#textures-weightimage)
- [Weight Image Layout](#textures-weightimage-layout)
- [Weight_Image_Layout](#textures-weightimage-layout)
- [2D Non-Separable Weight Filters](#_2d_non_separable_weight_filters)
- [2D_Non-Separable_Weight_Filters](#_2d_non_separable_weight_filters)
- [1D Separable Weight Filters](#_1d_separable_weight_filters)
- [1D_Separable_Weight_Filters](#_1d_separable_weight_filters)
- [Weight Sampling Phases](#textures-weightimage-filterphases)
- [Weight_Sampling_Phases](#textures-weightimage-filterphases)
- [Weight Sampler Parameters](#textures-weightimage-sampler)
- [Weight_Sampler_Parameters](#textures-weightimage-sampler)
- [Weight Sampling Operation](#textures-weightimage-filteroperation)
- [Weight_Sampling_Operation](#textures-weightimage-filteroperation)
- [Block Matching](#textures-blockmatch)
- [Block Matching Sampler Parameters](#textures-blockmatch-sampler)
- [Block_Matching_Sampler_Parameters](#textures-blockmatch-sampler)
- [Block Matching Operation](#textures-blockmatch-filteroperation)
- [Block_Matching_Operation](#textures-blockmatch-filteroperation)
- [Block Matching Window Operation](#textures-blockmatchwindow-filteroperation)
- [Block_Matching_Window_Operation](#textures-blockmatchwindow-filteroperation)
- [Block Matching Gather Operation](#textures-blockmatchgather-filteroperation)
- [Block_Matching_Gather_Operation](#textures-blockmatchgather-filteroperation)
- [Box Filter Sampling](#textures-boxfilter)
- [Box_Filter_Sampling](#textures-boxfilter)
- [Box Filter Sampler Parameters](#textures-boxfilter-sampler)
- [Box_Filter_Sampler_Parameters](#textures-boxfilter-sampler)
- [Box Filter Operation](#textures-boxfilter-filteroperation)
- [Box_Filter_Operation](#textures-boxfilter-filteroperation)
- [Image Operation Steps](#textures-instructions)
- [Image_Operation_Steps](#textures-instructions)
- [Image Query Instructions](#textures-queries)
- [Image_Query_Instructions](#textures-queries)
- [Image Property Queries](#_image_property_queries)
- [Image_Property_Queries](#_image_property_queries)
- [LOD Query](#_lod_query)

## Content

Vulkan Image Operations are operations performed by those SPIR-V Image
Instructions which take an `OpTypeImage` (representing a
`VkImageView`) or `OpTypeSampledImage` (representing a
(`VkImageView`, `VkSampler`) pair).
Read, write, and atomic operations also take texel coordinates as operands,
and return a value based on a neighborhood of texture elements (*texels*)
within the image.
Query operations return properties of the bound image or of the lookup
itself.
The “Depth” operand of `OpTypeImage` is ignored.

Image Operations include the functionality of the following SPIR-V Image
Instructions:

* 
`OpImageSample*` and `OpImageSparseSample*` read one or more
neighboring texels of the image, and [filter](#textures-texel-filtering)
the texel values based on the state of the sampler.

Instructions with `ImplicitLod` in the name
[determine](#textures-level-of-detail-operation) the LOD used in the
sampling operation based on the coordinates used in neighboring
fragments.

* 
Instructions with `ExplicitLod` in the name
[determine](#textures-level-of-detail-operation) the LOD used in the
sampling operation based on additional coordinates.

* 
Instructions with `Proj` in the name apply homogeneous
[projection](#textures-projection) to the coordinates.

`OpImageFetch` and `OpImageSparseFetch` return a single texel of
the image.
No sampler is used.

`OpImage*Gather` and `OpImageSparse*Gather` read neighboring
texels and [return a single component](#textures-gather) of each.

`OpImageRead` (and `OpImageSparseRead`) and `OpImageWrite` read
and write, respectively, a texel in the image.
No sampler is used.

`OpImageSampleFootprintNV` identifies and returns information about
the set of texels in the image that would be accessed by an equivalent
`OpImageSample*` instruction.

`OpImage*Dref*` instructions apply
[depth comparison](#textures-depth-compare-operation) on the texel
values.

`OpImageSparse*` instructions additionally return a
[sparse residency](#textures-sparse-residency) code.

`OpImageQuerySize`, `OpImageQuerySizeLod`,
`OpImageQueryLevels`, and `OpImageQuerySamples` return properties
of the image descriptor that would be accessed.
The image itself is not accessed.

`OpImageQueryLod` returns the LOD parameters that would be used in a
sample operation.
The actual operation is not performed.

`OpImageWeightedSampleQCOM` reads a 2D neighborhood of texels and
computes a weighted average using weight values from a separate weight
texture.

`opImageBlockMatchSADQCOM` and `opTextureBlockMatchSSD` compare 2D
neighborhoods of texels from two textures.

`OpImageBoxFilterQCOM` reads a 2D neighborhood of texels and computes
a weighted average of the texels.

`opImageBlockMatchWindowSADQCOM` and
`opImageBlockMatchWindowSSDQCOM` compare 2D neighborhoods of texels
from two textures with the comparison repeated across a window region in
the target texture.

`opImageBlockMatchGatherSADQCOM` and
`opImageBlockMatchWindowSSDQCOM` compares four 2D neighborhoods of
texels from a target texture with a single 2D neighborhood in the
reference texture.
The R component of each comparison is gathered and returned in the
output.

Images are addressed by *texel coordinates*.
There are three *texel coordinate systems*:

* 
normalized texel coordinates [0.0, 1.0]

* 
unnormalized texel coordinates [0.0, width / height / depth)

* 
integer texel coordinates [0, width / height / depth)

SPIR-V `OpImageFetch`, `OpImageSparseFetch`, `OpImageRead`,
`OpImageSparseRead`,
`opImageBlockMatchSADQCOM`, `opImageBlockMatchSSDQCOM`,
`opImageBlockMatchWindowSADQCOM`, `opImageBlockMatchWindowSSDQCOM`,
and `OpImageWrite` instructions use integer texel coordinates.

Other image instructions **can** use either normalized or unnormalized texel
coordinates (selected by the `unnormalizedCoordinates` state of the
sampler used in the instruction), but there are
[limitations](samplers.html#samplers-unnormalizedCoordinates) on what operations, image
state, and sampler state is supported.
Normalized coordinates are logically
[converted](#textures-normalized-to-unnormalized) to unnormalized as part of
image operations, and [certain steps](#textures-normalized-operations) are
only performed on normalized coordinates.
The array layer coordinate is always treated as unnormalized even when other
coordinates are normalized.

Normalized texel coordinates are referred to as (s,t,r,q,a), with the
coordinates having the following meanings:

* 
s: Coordinate in the first dimension of an image.

* 
t: Coordinate in the second dimension of an image.

* 
r: Coordinate in the third dimension of an image.

(s,t,r) are interpreted as a direction vector for Cube images.

q: Fourth coordinate, for homogeneous (projective) coordinates.

a: Coordinate for array layer.

The coordinates are extracted from the SPIR-V operand based on the
dimensionality of the image variable and type of instruction.
For `Proj` instructions, the components are in order (s, [t,] [r,]
q), with t and r being conditionally present based on the
`Dim` of the image.
For non-`Proj` instructions, the coordinates are (s [,t] [,r]
[,a]), with t and r being conditionally present based on the
`Dim` of the image and a being conditionally present based on the
`Arrayed` property of the image.
Projective image instructions are not supported on `Arrayed` images.

Unnormalized texel coordinates are referred to as (u,v,w,a), with the
coordinates having the following meanings:

* 
u: Coordinate in the first dimension of an image.

* 
v: Coordinate in the second dimension of an image.

* 
w: Coordinate in the third dimension of an image.

* 
a: Coordinate for array layer.

Only the u and v coordinates are directly extracted from the
SPIR-V operand, because only 1D and 2D (non-`Arrayed`) dimensionalities
support unnormalized coordinates.
The components are in order (u [,v]), with v being conditionally
present when the dimensionality is 2D.
When normalized coordinates are converted to unnormalized coordinates, all
four coordinates are used.

Integer texel coordinates are referred to as (i,j,k,l,n), with the
coordinates having the following meanings:

* 
i: Coordinate in the first dimension of an image.

* 
j: Coordinate in the second dimension of an image.

* 
k: Coordinate in the third dimension of an image.

* 
l: Coordinate for array layer.

* 
n: Index of the sample within the texel.

They are extracted from the SPIR-V operand in order (i [,j] [,k] [,l]
[,n]), with j and k conditionally present based on the `Dim`
of the image, and l conditionally present based on the `Arrayed`
property of the image.
n is conditionally present and is taken from the `Sample` image
operand.

If an accessed image was created from a view using
[VkImageViewSlicedCreateInfoEXT](resources.html#VkImageViewSlicedCreateInfoEXT) and accessed through a
`VK_DESCRIPTOR_TYPE_STORAGE_IMAGE` descriptor, then the value of k
is incremented by [VkImageViewSlicedCreateInfoEXT](resources.html#VkImageViewSlicedCreateInfoEXT)::`sliceOffset`,
giving k ← sliceOffset +  k.
The image’s accessible range in the third dimension is k .
If [VkImageViewSlicedCreateInfoEXT](resources.html#VkImageViewSlicedCreateInfoEXT)::`sliceCount` is
`VK_REMAINING_3D_SLICES_EXT`, the range is inherited from the image’s
depth extent as specified by [Image Mip Level Sizing](resources.html#resources-image-mip-level-sizing).

For all coordinate types, unused coordinates are assigned a value of zero.

![vulkantexture0 ll](../_images/vulkantexture0-ll.svg)

Figure 1. Texel Coordinate Systems, Linear Filtering

The Texel Coordinate Systems - For the example shown of an 8×4 texel
two dimensional image.

* 
Normalized texel coordinates:

The s coordinate goes from 0.0 to 1.0.

* 
The t coordinate goes from 0.0 to 1.0.

Unnormalized texel coordinates:

* 
The u coordinate within the range 0.0 to 8.0 is within the image,
otherwise it is outside the image.

* 
The v coordinate within the range 0.0 to 4.0 is within the image,
otherwise it is outside the image.

Integer texel coordinates:

* 
The i coordinate within the range 0 to 7 addresses texels within
the image, otherwise it is outside the image.

* 
The j coordinate within the range 0 to 3 addresses texels within
the image, otherwise it is outside the image.

Also shown for linear filtering:

* 
Given the unnormalized coordinates (u,v), the four texels
selected are i0j0, i1j0, i0j1, and
i1j1.

* 
The fractions α and β.

* 
Given the offset Δi and Δj, the
four texels selected by the offset are i0j'0,
i1j'0, i0j'1, and i1j'1.

![vulkantexture1 ll](../_images/vulkantexture1-ll.svg)

Figure 2. Texel Coordinate Systems, Nearest Filtering

The Texel Coordinate Systems - For the example shown of an 8×4 texel
two dimensional image.

* 
Texel coordinates as above.
Also shown for nearest filtering:

Given the unnormalized coordinates (u,v), the texel selected is
ij.

* 
Given the offset Δi and Δj, the
texel selected by the offset is ij'.

For corner-sampled images, the texel samples are located at the grid
intersections instead of the texel centers.

![vulkantexture0 corner alternative a ll](../_images/vulkantexture0-corner-alternative-a-ll.svg)

Figure 3. Texel Coordinate Systems, Corner Sampling

An RGB color (red, green, blue) is transformed to a shared exponent
color (redshared, greenshared, blueshared, expshared) as
follows:

First, the components (red, green, blue) are clamped to
(redclamped, greenclamped, blueclamped) as:

redclamped = max(0, min(sharedexpmax, red))

greenclamped = max(0, min(sharedexpmax, green))

blueclamped = max(0, min(sharedexpmax, blue))

where:

  

  

The largest clamped component, maxclamped is determined:

maxclamped = max(redclamped, greenclamped,
blueclamped)

A preliminary shared exponent exp' is computed:

  

  

The shared exponent expshared is computed:

  

  

  

  

Finally, three integer values in the range 0 to 2N are
computed:

  

  

A shared exponent color (redshared, greenshared, blueshared,
expshared) is transformed to an RGB color (red, green, blue) as
follows:

  

\(green = green_{shared} \times
{2^{(exp_{shared}-B-N)}}\)

  

where:

N = 9 (number of mantissa bits per component)

B = 15 (exponent bias)

*Texel input instructions* are SPIR-V image instructions that read from an
image.
*Texel input operations* are a set of steps that are performed on state,
coordinates, and texel values while processing a texel input instruction,
and which are common to some or all texel input instructions.
They include the following steps, which are performed in the listed order:

* 
[Validation operations](#textures-input-validation)

[Instruction/Sampler/Image validation](#textures-operation-validation)

* 
[Coordinate validation](#textures-integer-coordinate-validation)

* 
[Sparse validation](#textures-sparse-validation)

* 
[Layout validation](#textures-layout-validation)

[Format conversion](#textures-format-conversion)

[Texel replacement](#textures-texel-replacement)

[Depth comparison](#textures-depth-compare-operation)

[Conversion to RGBA](#textures-conversion-to-rgba)

[Component swizzle](#textures-component-swizzle)

[Chroma reconstruction](#textures-chroma-reconstruction)

[Y′CBCR conversion](#textures-sampler-YCbCr-conversion)

For texel input instructions involving multiple texels (for sampling or
gathering), these steps are applied for each texel that is used in the
instruction.
Depending on the type of image instruction, other steps are conditionally
performed between these steps or involving multiple coordinate or texel
values.

If [Chroma Reconstruction](#textures-chroma-reconstruction) is implicit,
[Texel Filtering](#textures-texel-filtering) instead takes place during
chroma reconstruction, before [sampler Y′CBCR conversion](#textures-sampler-YCbCr-conversion) occurs.

The operations described in [block matching](#textures-blockmatch) and
[weight image sampling](#textures-weightimage) are performed before
[Conversion to RGBA](#textures-conversion-to-rgba) and
[Component swizzle](#textures-component-swizzle).

*Texel input validation operations* inspect instruction/image/sampler state
or coordinates, and in certain circumstances cause the texel value to be
replaced or become **undefined**.
There are a series of validations that the texel undergoes.

There are a number of cases where a SPIR-V instruction **can** mismatch with
the sampler, the image view, or both, and a number of further cases where
the sampler **can** mismatch with the image view.
In such cases the value of the texel returned is **undefined**.

These cases include:

* 
The sampler `borderColor` is an integer type and the image view
`format` is not one of the [VkFormat](formats.html#VkFormat) integer types or a stencil
component of a depth/stencil format.

* 
The sampler `borderColor` is a float type and the image view
`format` is not one of the [VkFormat](formats.html#VkFormat) float types or a depth
component of a depth/stencil format.

* 
The sampler `borderColor` is one of the opaque black colors
(`VK_BORDER_COLOR_FLOAT_OPAQUE_BLACK` or
`VK_BORDER_COLOR_INT_OPAQUE_BLACK`) and the image view
[VkComponentSwizzle](resources.html#VkComponentSwizzle) for any of the [VkComponentMapping](resources.html#VkComponentMapping)
components is not the [identity    swizzle](resources.html#resources-image-views-identity-mappings), and
[VkPhysicalDeviceBorderColorSwizzleFeaturesEXT](features.html#VkPhysicalDeviceBorderColorSwizzleFeaturesEXT)::`borderColorSwizzleFromImage`
feature is not enabled, and
[VkSamplerBorderColorComponentMappingCreateInfoEXT](samplers.html#VkSamplerBorderColorComponentMappingCreateInfoEXT) is not
specified.

* 
[VkSamplerBorderColorComponentMappingCreateInfoEXT](samplers.html#VkSamplerBorderColorComponentMappingCreateInfoEXT)::`components`,
if specified, has a component swizzle that does not match the component
swizzle of the image view, and either component swizzle is not a form of
identity swizzle.

* 
[VkSamplerBorderColorComponentMappingCreateInfoEXT](samplers.html#VkSamplerBorderColorComponentMappingCreateInfoEXT)::`srgb`, if
specified, does not match the sRGB encoding of the image view.

* 
The sampler `borderColor` is a custom color
(`VK_BORDER_COLOR_FLOAT_CUSTOM_EXT` or
`VK_BORDER_COLOR_INT_CUSTOM_EXT`) and the supplied
[VkSamplerCustomBorderColorCreateInfoEXT](samplers.html#VkSamplerCustomBorderColorCreateInfoEXT)::`customBorderColor`
is outside the bounds of the values representable in the image view’s
`format`.

* 
The sampler `borderColor` is a custom color
(`VK_BORDER_COLOR_FLOAT_CUSTOM_EXT` or
`VK_BORDER_COLOR_INT_CUSTOM_EXT`) and the image view
[VkComponentSwizzle](resources.html#VkComponentSwizzle) for any of the [VkComponentMapping](resources.html#VkComponentMapping)
components is not the [identity    swizzle](resources.html#resources-image-views-identity-mappings), and
[VkPhysicalDeviceBorderColorSwizzleFeaturesEXT](features.html#VkPhysicalDeviceBorderColorSwizzleFeaturesEXT)::`borderColorSwizzleFromImage`
feature is not enabled, and
[VkSamplerBorderColorComponentMappingCreateInfoEXT](samplers.html#VkSamplerBorderColorComponentMappingCreateInfoEXT) is not
specified.

* 
The [VkImageLayout](resources.html#VkImageLayout) of any subresource in the image view does not
match the [VkDescriptorImageInfo](descriptorsets.html#VkDescriptorImageInfo)::`imageLayout` used to write
the image descriptor.

* 
The SPIR-V Image Format is not [compatible](../appendices/spirvenv.html#spirvenv-image-formats)
with the image view’s `format`.

* 
The sampler `unnormalizedCoordinates` is `VK_TRUE` and any of
the [limitations of unnormalized    coordinates](samplers.html#samplers-unnormalizedCoordinates) are violated.

* 
The sampler was created with `flags` containing
`VK_SAMPLER_CREATE_SUBSAMPLED_BIT_EXT` and the image was not created
with `flags` containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`.

* 
The sampler was not created with `flags` containing
`VK_SAMPLER_CREATE_SUBSAMPLED_BIT_EXT` and the image was created
with `flags` containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`.

* 
The sampler was created with `flags` containing
`VK_SAMPLER_CREATE_SUBSAMPLED_BIT_EXT` and is used with a function
that is not `OpImageSampleImplicitLod` or
`OpImageSampleExplicitLod`, or is used with operands `Offset` or
`ConstOffsets`.

* 
The SPIR-V instruction is one of the `OpImage*Dref*` instructions and
the sampler `compareEnable` is `VK_FALSE`

* 
The SPIR-V instruction is not one of the `OpImage*Dref*` instructions
and the sampler `compareEnable` is `VK_TRUE`

* 
The SPIR-V instruction is one of the `OpImage*Dref*` instructions,
the image view `format` is one of the depth/stencil formats, and the
image view aspect is not `VK_IMAGE_ASPECT_DEPTH_BIT`.

* 
The SPIR-V instruction’s image variable’s properties are not compatible
with the image view:

If the image view’s `viewType` is one of
`VK_IMAGE_VIEW_TYPE_1D_ARRAY`, `VK_IMAGE_VIEW_TYPE_2D_ARRAY`,
or `VK_IMAGE_VIEW_TYPE_CUBE_ARRAY` then the instruction **must** have
`Arrayed` = 1.
Otherwise the instruction **must** have `Arrayed` = 0.

* 
If the image was created with [VkImageCreateInfo](resources.html#VkImageCreateInfo)::`samples`
equal to `VK_SAMPLE_COUNT_1_BIT`, the instruction **must** have
`MS` = 0.

* 
If the image was created with [VkImageCreateInfo](resources.html#VkImageCreateInfo)::`samples`
not equal to `VK_SAMPLE_COUNT_1_BIT`, the instruction **must** have
`MS` = 1.

* 
If the `Sampled` `Type` of the `OpTypeImage` does not match
the [SPIR-V Type](../appendices/spirvenv.html#spirv-type).

* 
If the [signedness of any read or sample     operation](../appendices/spirvenv.html#spirvenv-image-signedness) does not match the signedness of the image’s format.

If the image was created with [VkImageCreateInfo](resources.html#VkImageCreateInfo)::`flags`
containing `VK_IMAGE_CREATE_CORNER_SAMPLED_BIT_NV`, the sampler
addressing modes **must** only use a [VkSamplerAddressMode](samplers.html#VkSamplerAddressMode) of
`VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_EDGE`.

The SPIR-V instruction is `OpImageSampleFootprintNV` with `Dim` =
2D and `addressModeU` or `addressModeV` in the sampler is not
`VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_EDGE`.

The SPIR-V instruction is `OpImageSampleFootprintNV` with `Dim` =
3D and `addressModeU`, `addressModeV`, or `addressModeW` in
the sampler is not `VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_EDGE`.

The sampler was created with a specified
[VkSamplerCustomBorderColorCreateInfoEXT](samplers.html#VkSamplerCustomBorderColorCreateInfoEXT)::`format` which does
not match the [VkFormat](formats.html#VkFormat) of the image view(s) it is sampling.

The sampler is sampling an image view of
`VK_FORMAT_B4G4R4A4_UNORM_PACK16`,
`VK_FORMAT_B5G6R5_UNORM_PACK16`, or
`VK_FORMAT_B5G5R5A1_UNORM_PACK16` format without a specified
[VkSamplerCustomBorderColorCreateInfoEXT](samplers.html#VkSamplerCustomBorderColorCreateInfoEXT)::`format`.

Only `OpImageSample*` and `OpImageSparseSample*` **can** be used with a
sampler or image view that enables [sampler Y′CBCR conversion](samplers.html#samplers-YCbCr-conversion).

`OpImageFetch`, `OpImageSparseFetch`, `OpImage*Gather`, and
`OpImageSparse*Gather` **must** not be used with a sampler or image view
that enables [sampler Y′CBCR conversion](samplers.html#samplers-YCbCr-conversion).

The `ConstOffset` and `Offset` operands **must** not be used with a
sampler or image view that enables [sampler Y′CBCR conversion](samplers.html#samplers-YCbCr-conversion).

If the underlying `VkImage` format has an X component in its format
description, **undefined** values are read from those bits.

Integer texel coordinates are validated against the size of the image level,
and the number of layers and number of samples in the image.
For SPIR-V instructions that use integer texel coordinates, this is
performed directly on the integer coordinates.
For instructions that use normalized or unnormalized texel coordinates, this
is performed on the coordinates that result after
[conversion](#textures-unnormalized-to-integer) to integer texel
coordinates.

If the integer texel coordinates do not satisfy all of the conditions

0 ≤ i s

0 ≤ j s

0 ≤ k s

0 ≤ l 

0 ≤ n 

where:

ws = width of the image level

hs = height of the image level

ds = depth of the image level

layers = number of layers in the image

samples = number of samples per texel in the image

then the texel fails integer texel coordinate validation.

There are four cases to consider:

Valid Texel Coordinates

* 
If the texel coordinates pass validation (that is, the coordinates lie
within the image),

then the texel value comes from the value in image memory.

Border Texel

* 
If the texel coordinates fail validation, and

* 
If the read is the result of an image sample instruction or image gather
instruction, and

* 
If the image is not a cube image,
or if a sampler created with
`VK_SAMPLER_CREATE_NON_SEAMLESS_CUBE_MAP_BIT_EXT` is used,

then the texel is a border texel and [texel replacement](#textures-texel-replacement) is performed.

Invalid Texel

* 
If the texel coordinates fail validation, and

* 
If the read is the result of an image fetch instruction, image read
instruction, or atomic instruction,

then the texel is an invalid texel and [texel replacement](#textures-texel-replacement) is performed.

Cube Map Edge or Corner

Otherwise the texel coordinates lie beyond the edges or corners of the
selected cube map face, and [Cube map edge handling](#textures-cubemapedge)
is performed.

If the texel coordinates lie beyond the edges or corners of the selected
cube map face (as described in the prior section), the following steps are
performed.
Note that this does not occur when using `VK_FILTER_NEAREST` filtering
within a mip level, since `VK_FILTER_NEAREST` is treated as using
`VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_EDGE`.

* 
Cube Map Edge Texel

If the texel lies beyond the selected cube map face in either only
i or only j, then the coordinates (i,j) and the array
layer l are transformed to select the adjacent texel from the
appropriate neighboring face.

Cube Map Corner Texel

* 
If the texel lies beyond the selected cube map face in both i and
     j, then there is no unique neighboring face from which to read
     that texel.
     The texel **should** be replaced by the average of the three values of the
     adjacent texels in each incident face.
     However, implementations **may** replace the cube map corner texel by
     other methods.
The methods are subject to the constraint that for linear filtering if the
three available texels have the same value, the resulting filtered texel
**must** have that value, and for cubic filtering if the twelve available
samples have the same value, the resulting filtered texel **must** have that
value.

If the texel reads from an unbound region of a sparse image, the texel is a
*sparse unbound texel*, and processing continues with
[texel replacement](#textures-texel-replacement).

If all planes of a *disjoint* *multi-planar* image are not in the same
[image layout](resources.html#resources-image-layouts), the image **must** not be sampled
with [sampler Y′CBCR conversion](samplers.html#samplers-YCbCr-conversion) enabled.

Texels undergo a format conversion from the [VkFormat](formats.html#VkFormat) of the image view
to a vector of either floating-point or signed or unsigned integer
components, with the number of components based on the number of components
present in the format.

* 
Color formats have one, two, three, or four components, according to the
format.

* 
Depth/stencil formats are one component.
The depth or stencil component is selected by the `aspectMask` of
the image view.

Each component is converted based on its type and size (as defined in the
[Format Definition](formats.html#formats-definition) section for each [VkFormat](formats.html#VkFormat)),
using the appropriate equations in [16-Bit Floating-Point Numbers](fundamentals.html#fundamentals-fp16), [Unsigned 11-Bit Floating-Point Numbers](fundamentals.html#fundamentals-fp11),
[Unsigned 10-Bit Floating-Point Numbers](fundamentals.html#fundamentals-fp10),
[Fixed-Point Data Conversion](fundamentals.html#fundamentals-fixedconv), and
[Shared Exponent to RGB](#textures-sexp-RGB).
Signed integer components smaller than 32 bits are sign-extended.

If the image view format is sRGB, the color components are first converted
as if they are UNORM, and then sRGB to linear conversion is applied to the
R, G, and B components as described in the “sRGB EOTF” section of the
[Khronos Data Format Specification](introduction.html#data-format).
The A component, if present, is unchanged.

If
[VkSamplerYcbcrConversionYcbcrDegammaCreateInfoQCOM](samplers.html#VkSamplerYcbcrConversionYcbcrDegammaCreateInfoQCOM)::`enableYDegamma`
is equal to `VK_TRUE`, then sRGB to linear conversion is applied to the
G component as described in the “sRGB EOTF” section of the
[Khronos Data Format Specification](introduction.html#data-format).
If
[VkSamplerYcbcrConversionYcbcrDegammaCreateInfoQCOM](samplers.html#VkSamplerYcbcrConversionYcbcrDegammaCreateInfoQCOM)::`enableCbCrDegamma`
is equal to `VK_TRUE`, then sRGB to linear conversion is applied to the
R and B components as described in the “sRGB EOTF” section of the
[Khronos Data Format Specification](introduction.html#data-format).
The A component, if present, is unchanged.

If the image view format is block-compressed, then the texel value is first
decoded, then converted based on the type and number of components defined
by the compressed format.

A texel is replaced if it is one (and only one) of:

* 
a border texel,

* 
an invalid texel, or

* 
a sparse unbound texel.

Border texels are replaced with a value based on the image format and the
`borderColor` of the sampler.
The border color is:

Table 1. Border Color B, Custom Border Color [VkSamplerCustomBorderColorCreateInfoEXT](samplers.html#VkSamplerCustomBorderColorCreateInfoEXT)::`customBorderColor` U

Sampler `borderColor`
Corresponding Border Color

`VK_BORDER_COLOR_FLOAT_TRANSPARENT_BLACK`
[Br, Bg, Bb, Ba] = [0.0, 0.0, 0.0, 0.0]

`VK_BORDER_COLOR_FLOAT_OPAQUE_BLACK`
[Br, Bg, Bb, Ba] = [0.0, 0.0, 0.0, 1.0]

`VK_BORDER_COLOR_FLOAT_OPAQUE_WHITE`
[Br, Bg, Bb, Ba] = [1.0, 1.0, 1.0, 1.0]

`VK_BORDER_COLOR_INT_TRANSPARENT_BLACK`
[Br, Bg, Bb, Ba] = [0, 0, 0, 0]

`VK_BORDER_COLOR_INT_OPAQUE_BLACK`
[Br, Bg, Bb, Ba] = [0, 0, 0, 1]

`VK_BORDER_COLOR_INT_OPAQUE_WHITE`
[Br, Bg, Bb, Ba] = [1, 1, 1, 1]

`VK_BORDER_COLOR_FLOAT_CUSTOM_EXT`
[Br, Bg, Bb, Ba] = [Ur, Ug, Ub, Ua]

`VK_BORDER_COLOR_INT_CUSTOM_EXT`
[Br, Bg, Bb, Ba] = [Ur, Ug, Ub, Ua]

The custom border color (U) **may** be rounded by implementations prior
to texel replacement, but the error introduced by such a rounding **must** not
exceed one ULP of the image’s `format`.

This is substituted for the texel value by replacing the number of
components in the image format

Table 2. Border Texel Components After Replacement

Texel Aspect or Format
Component Assignment

Depth aspect
D                                     = Br

Stencil aspect
S                                     = Br†

One component color format
Colorr                              = Br

Two component color format
[Colorr,Colorg]                   = [Br,Bg]

Three component color format
[Colorr,Colorg,Colorb]          = [Br,Bg,Bb]

Four component color format
[Colorr,Colorg,Colorb,Colora] = [Br,Bg,Bb,Ba]

Single component alpha format
[Colorr,Colorg,Colorb, Colora] = [0,0,0,Ba]

† S = Bg **may** be substituted as the replacement method by the
implementation when [VkSamplerCreateInfo](samplers.html#VkSamplerCreateInfo)::`borderColor` is
`VK_BORDER_COLOR_INT_CUSTOM_EXT` and
[VkSamplerCustomBorderColorCreateInfoEXT](samplers.html#VkSamplerCustomBorderColorCreateInfoEXT)::`format` is
`VK_FORMAT_UNDEFINED`.
Implementations **should** use S = Br as the replacement method.

The value returned by a read of an invalid texel is **undefined**, unless that
read operation is from a buffer resource and the
[`robustBufferAccess`](features.html#features-robustBufferAccess) feature is
enabled.
In that case, an invalid texel is replaced as described by the
[`robustBufferAccess`](features.html#features-robustBufferAccess) feature.
If the access is to an image resource and the x, y, z, or layer coordinate
validation fails and
the [`robustImageAccess`](features.html#features-robustImageAccess) feature is
enabled, then zero **must** be returned for the R, G, and B components, if
present.
Either zero or one **must** be returned for the A component, if present.
If the [`robustImageAccess2`](features.html#features-robustImageAccess2) feature is
enabled, zero values **must** be returned.
If only the sample index was invalid, the values returned are **undefined**.

Additionally, if the [`robustImageAccess`](features.html#features-robustImageAccess)
feature is enabled,
but the [`robustImageAccess2`](features.html#features-robustImageAccess2) feature is
not,
any invalid texels **may** be expanded to four components prior to texel
replacement.
This means that components not present in the image format may be replaced
with 0 or may undergo [conversion to RGBA](#textures-conversion-to-rgba) as
normal.

Loads from a null descriptor return a four component color value of all
zeros.
However, for storage images and storage texel buffers using an explicit
SPIR-V Image Format, loads from a null descriptor **may** return an alpha value
of 1 (float or integer, depending on format) if the format does not include
alpha.

If the
[VkPhysicalDeviceSparseProperties](sparsemem.html#VkPhysicalDeviceSparseProperties)::`residencyNonResidentStrict`
property is `VK_TRUE`, a sparse unbound texel is replaced with 0 or 0.0
values for integer and floating-point components of the image format,
respectively.

If `residencyNonResidentStrict` is `VK_FALSE`, the value of the
sparse unbound texel is **undefined**.

If the image view has a depth/stencil format, the depth component is
selected by the `aspectMask`, and the operation is an `OpImage*Dref*`
instruction, a depth comparison is performed.
The result is 1.0 if the comparison evaluates to true, and
0.0 otherwise.
This value replaces the depth component D.

The compare operation is selected by the [VkCompareOp](samplers.html#VkCompareOp) value set by
[VkSamplerCreateInfo](samplers.html#VkSamplerCreateInfo)::`compareOp`.
The reference value from the SPIR-V operand Dref and the texel depth
value Dtex are used as the *reference* and *test* values,
respectively, in that operation.

If the image being sampled has an unsigned normalized fixed-point format,
then Dref is clamped to [0,1] before the compare operation.

If the value of `magFilter` is `VK_FILTER_LINEAR`, or the value of
`minFilter` is `VK_FILTER_LINEAR`, then D may be computed in
an implementation-dependent manner which differs from the normal rules of
linear filtering.
The resulting value **must** be in the range [0,1] and should be
proportional to, or a weighted average of, the number of comparison passes
or failures.

The texel is expanded from one, two, or three components to four components
based on the image base color:

Table 3. Texel Color After Conversion To RGBA

Texel Aspect or Format
RGBA Color

Depth aspect
[Colorr,Colorg,Colorb, Colora] = [D,0,0,one]

Stencil aspect
[Colorr,Colorg,Colorb, Colora] = [S,0,0,one]

One component color format
[Colorr,Colorg,Colorb, Colora] = [Colorr,0,0,one]

Two component color format
[Colorr,Colorg,Colorb, Colora] = [Colorr,Colorg,0,one]

Three component color format
[Colorr,Colorg,Colorb, Colora] = [Colorr,Colorg,Colorb,one]

Four component color format
[Colorr,Colorg,Colorb, Colora] = [Colorr,Colorg,Colorb,Colora]

One alpha component color format
[Colorr,Colorg,Colorb, Colora] = [0,0,0,Colora]

where one = 1.0f for floating-point formats and depth aspects, and
one = 1 for integer formats and stencil aspects.

All texel input instructions apply a *swizzle* based on:

* 
the [VkComponentSwizzle](resources.html#VkComponentSwizzle) enums in the `components` member of the
[VkImageViewCreateInfo](resources.html#VkImageViewCreateInfo) structure for the image being read if
[sampler Y′CBCR conversion](samplers.html#samplers-YCbCr-conversion) is not enabled,
and

* 
the [VkComponentSwizzle](resources.html#VkComponentSwizzle) enums in the `components` member of the
[VkSamplerYcbcrConversionCreateInfo](samplers.html#VkSamplerYcbcrConversionCreateInfo) structure for the
[sampler Y′CBCR conversion](samplers.html#samplers-YCbCr-conversion) if sampler
Y′CBCR conversion is enabled.

The swizzle **can** rearrange the components of the texel, or substitute zero
or one for any components.
It is defined as follows for each color component:

  

  

where:

  

  

If the border color is one of the `VK_BORDER_COLOR_*_OPAQUE_BLACK` enums
and the [VkComponentSwizzle](resources.html#VkComponentSwizzle) is not the
[identity swizzle](resources.html#resources-image-views-identity-mappings) for all
components, the value of the texel after swizzle is **undefined**.

If the image view has a depth/stencil format and the
[VkComponentSwizzle](resources.html#VkComponentSwizzle) is `VK_COMPONENT_SWIZZLE_ONE`, and
`VkPhysicalDeviceMaintenance5Properties`::`depthStencilSwizzleOneSupport`
is not `VK_TRUE`, the value of the texel after swizzle is **undefined**.

`OpImageSparse*` instructions return a structure which includes a
*residency code* indicating whether any texels accessed by the instruction
are sparse unbound texels.
This code **can** be interpreted by the `OpImageSparseTexelsResident`
instruction which converts the residency code to a boolean value.

In some color models, the color representation is defined in terms of
monochromatic light intensity (often called “luma”) and color differences
relative to this intensity, often called “chroma”.
It is common for color models other than RGB to represent the chroma
components at lower spatial resolution than the luma component.
This approach is used to take advantage of the eye’s lower spatial
sensitivity to color compared with its sensitivity to brightness.
Less commonly, the same approach is used with additive color, since the
green component dominates the eye’s sensitivity to light intensity and the
spatial sensitivity to color introduced by red and blue is lower.

Lower-resolution components are “downsampled” by resizing them to a lower
spatial resolution than the component representing luminance.
This process is also commonly known as “chroma subsampling”.
There is one luminance sample in each texture texel, but each chrominance
sample may be shared among several texels in one or both texture dimensions.

* 
“`_444`” formats do not spatially downsample chroma values
compared with luma: there are unique chroma samples for each texel.

* 
“`_422`” formats have downsampling in the x dimension
(corresponding to *u* or *s* coordinates): they are sampled at half the
resolution of luma in that dimension.

* 
“`_420`” formats have downsampling in the x dimension
(corresponding to *u* or *s* coordinates) and the y dimension
(corresponding to *v* or *t* coordinates): they are sampled at half the
resolution of luma in both dimensions.

The process of reconstructing a full color value for texture access involves
accessing both chroma and luma values at the same location.
To generate the color accurately, the values of the lower-resolution
components at the location of the luma samples are reconstructed from the
lower-resolution sample locations, an operation known here as “chroma
reconstruction” irrespective of the actual color model.

The location of the chroma samples relative to the luma coordinates is
determined by the `xChromaOffset` and `yChromaOffset` members of the
[VkSamplerYcbcrConversionCreateInfo](samplers.html#VkSamplerYcbcrConversionCreateInfo) structure used to create the
sampler Y′CBCR conversion.

The following diagrams show the relationship between unnormalized (*u*,*v*)
coordinates and (*i*,*j*) integer texel positions in the luma component
(shown in black, with circles showing integer sample positions) and the
texel coordinates of reduced-resolution chroma components, shown as crosses
in red.

![chromasamples 422 cosited](../_images/chromasamples_422_cosited.svg)

Figure 4. 422 downsampling, xChromaOffset=COSITED_EVEN

![chromasamples 422 midpoint](../_images/chromasamples_422_midpoint.svg)

Figure 5. 422 downsampling, xChromaOffset=MIDPOINT

![chromasamples 420 xcosited ycosited](../_images/chromasamples_420_xcosited_ycosited.svg)

Figure 6. 420 downsampling, xChromaOffset=COSITED_EVEN, yChromaOffset=COSITED_EVEN

![chromasamples 420 xmidpoint ycosited](../_images/chromasamples_420_xmidpoint_ycosited.svg)

Figure 7. 420 downsampling, xChromaOffset=MIDPOINT, yChromaOffset=COSITED_EVEN

![chromasamples 420 xcosited ymidpoint](../_images/chromasamples_420_xcosited_ymidpoint.svg)

Figure 8. 420 downsampling, xChromaOffset=COSITED_EVEN, yChromaOffset=MIDPOINT

![chromasamples 420 xmidpoint ymidpoint](../_images/chromasamples_420_xmidpoint_ymidpoint.svg)

Figure 9. 420 downsampling, xChromaOffset=MIDPOINT, yChromaOffset=MIDPOINT

Reconstruction is implemented in one of two ways:

If the format of the image that is to be sampled sets
`VK_FORMAT_FEATURE_SAMPLED_IMAGE_YCBCR_CONVERSION_CHROMA_RECONSTRUCTION_EXPLICIT_BIT`,
or the [VkSamplerYcbcrConversionCreateInfo](samplers.html#VkSamplerYcbcrConversionCreateInfo)’s
`forceExplicitReconstruction` is `VK_TRUE`, reconstruction is
performed as an explicit step independent of filtering, described in the
[Explicit Reconstruction](#textures-explicit-reconstruction) section.

If the format of the image that is to be sampled does not set
`VK_FORMAT_FEATURE_SAMPLED_IMAGE_YCBCR_CONVERSION_CHROMA_RECONSTRUCTION_EXPLICIT_BIT`
and if the [VkSamplerYcbcrConversionCreateInfo](samplers.html#VkSamplerYcbcrConversionCreateInfo)’s
`forceExplicitReconstruction` is `VK_FALSE`, reconstruction is
performed as an implicit part of filtering prior to color model conversion,
with no separate post-conversion texel filtering step, as described in the
[Implicit Reconstruction](#textures-implict-reconstruction) section.

* 
If the `chromaFilter` member of the
[VkSamplerYcbcrConversionCreateInfo](samplers.html#VkSamplerYcbcrConversionCreateInfo) structure is
`VK_FILTER_NEAREST`:

If the format’s R and B components are reduced in resolution in just
width by a factor of two relative to the G component (i.e. this is a
“`_422`” format), the    values
accessed by [texel filtering](#textures-texel-filtering) are
reconstructed as follows:

  

  

* 
If the format’s R and B components are reduced in resolution in width
and height by a factor of two relative to the G component (i.e. this is
a “`_420`” format), the    values
accessed by [texel filtering](#textures-texel-filtering) are
reconstructed as follows:

  

  

If the `chromaFilter` member of the
[VkSamplerYcbcrConversionCreateInfo](samplers.html#VkSamplerYcbcrConversionCreateInfo) structure is
`VK_FILTER_LINEAR`:

* 
If the format’s R and B components are reduced in resolution in just
width by a factor of two relative to the G component (i.e. this is a
“`_422`” format):

If `xChromaOffset` is `VK_CHROMA_LOCATION_COSITED_EVEN`:

  

  

* 
If `xChromaOffset` is `VK_CHROMA_LOCATION_MIDPOINT`:

  

  

If the format’s R and B components are reduced in resolution in width
and height by a factor of two relative to the G component (i.e. this is
a “`_420`” format), a similar relationship applies.
Due to the number of options, these formulae are expressed more
concisely as follows:

  

  

  

  

Implicit reconstruction takes place by the samples being interpolated, as
required by the filter settings of the sampler, except that
`chromaFilter` takes precedence for the chroma samples.

If `chromaFilter` is `VK_FILTER_NEAREST`, an implementation **may**
behave as if `xChromaOffset` and `yChromaOffset` were both
`VK_CHROMA_LOCATION_MIDPOINT`, irrespective of the values set.

The sample coordinates are adjusted by the downsample factor of the
component (such that, for example, the sample coordinates are divided by two
if the component has a downsample factor of two relative to the luma
component):

  

  

Sampler Y′CBCR conversion performs the following operations, which an
implementation **may** combine into a single mathematical operation:

* 
[Sampler Y′CBCR Range    Expansion](#textures-sampler-YCbCr-conversion-rangeexpand)

* 
[Sampler Y′CBCR    Model Conversion](#textures-sampler-YCbCr-conversion-modelconversion)

Sampler Y′CBCR range expansion is applied to color component values after
all texel input operations which are not specific to sampler Y′CBCR
conversion.
For example, the input values to this stage have been converted using the
normal [format conversion](#textures-format-conversion) rules.

The input values to this stage may have been converted using sRGB to linear
conversion if the [`ycbcrDegamma`](features.html#features-ycbcrDegamma) feature is
enabled.

Sampler Y′CBCR range expansion is not applied if `ycbcrModel` is
`VK_SAMPLER_YCBCR_MODEL_CONVERSION_RGB_IDENTITY`.
That is, the shader receives the vector C'rgba as output by the Component
Swizzle stage without further modification.

For other values of `ycbcrModel`, range expansion is applied to the
texel component values output by the [Component Swizzle](#textures-component-swizzle) defined by the `components` member of
[VkSamplerYcbcrConversionCreateInfo](samplers.html#VkSamplerYcbcrConversionCreateInfo).
Range expansion applies independently to each component of the image.
For the purposes of range expansion and Y′CBCR model conversion, the R and
B components contain color difference (chroma) values and the G component
contains luma.
The A component is not modified by sampler Y′CBCR range expansion.

The range expansion to be applied is defined by the `ycbcrRange` member
of the [VkSamplerYcbcrConversionCreateInfo](samplers.html#VkSamplerYcbcrConversionCreateInfo) structure:

* 
If `ycbcrRange` is `VK_SAMPLER_YCBCR_RANGE_ITU_FULL`, the
following transformations are applied:

  

  

* 
If `ycbcrRange` is `VK_SAMPLER_YCBCR_RANGE_ITU_NARROW`, the
following transformations are applied:

  

  

* 
*n* is the bit-depth of the components in the format.

The precision of the operations performed during range expansion **must** be at
least that of the source format.

An implementation **may** clamp the results of these range expansion operations
such that Y′ falls in the range [0,1], and/or such that CB and CR
fall in the range [-0.5,0.5].

The range-expanded values are converted between color models, according to
the color model conversion specified in the `ycbcrModel` member:

`VK_SAMPLER_YCBCR_MODEL_CONVERSION_RGB_IDENTITY`

The color components are not modified by the color model conversion
since they are assumed already to represent the desired color model in
which the shader is operating; Y′CBCR range expansion is also ignored.

`VK_SAMPLER_YCBCR_MODEL_CONVERSION_YCBCR_IDENTITY`

The color components are not modified by the color model conversion and
are assumed to be treated as though in Y′CBCR form both in memory and
in the shader; Y′CBCR range expansion is applied to the components as
for other Y′CBCR models, with the vector (CR,Y′,CB,A)
provided to the shader.

`VK_SAMPLER_YCBCR_MODEL_CONVERSION_YCBCR_709`

The color components are transformed from a Y′CBCR representation to an
R′G′B′ representation as described in the “BT.709 Y′CBCR
conversion” section of the [Khronos Data Format    Specification](introduction.html#data-format).

`VK_SAMPLER_YCBCR_MODEL_CONVERSION_YCBCR_601`

The color components are transformed from a Y′CBCR representation to an
R′G′B′ representation as described in the “BT.601 Y′CBCR
conversion” section of the [Khronos Data Format    Specification](introduction.html#data-format).

`VK_SAMPLER_YCBCR_MODEL_CONVERSION_YCBCR_2020`

The color components are transformed from a Y′CBCR representation to an
R′G′B′ representation as described in the “BT.2020 Y′CBCR
conversion” section of the [Khronos Data Format    Specification](introduction.html#data-format).

In this operation, each output component is dependent on each input
component.

An implementation **may** clamp the R′G′B′ results of these conversions to
the range [0,1].

The precision of the operations performed during model conversion **must** be
at least that of the source format.

The alpha component is not modified by these model conversions.

*Texel output instructions* are SPIR-V image instructions that write to an
image.
*Texel output operations* are a set of steps that are performed on state,
coordinates, and texel values while processing a texel output instruction,
and which are common to some or all texel output instructions.
They include the following steps, which are performed in the listed order:

* 
[Validation operations](#textures-output-validation)

[Format validation](#textures-format-validation)

* 
[Type validation](#textures-type-validation)

* 
[Coordinate validation](#textures-output-coordinate-validation)

* 
[Sparse validation](#textures-output-sparse-validation)

[Texel output format conversion](#textures-output-format-conversion)

*Texel output validation operations* inspect instruction/image state or
coordinates, and in certain circumstances cause the write to have no effect.
There are a series of validations that the texel undergoes.

If the image format of the `OpTypeImage` is not
[compatible](../appendices/spirvenv.html#spirvenv-image-formats) with the `VkImageView`’s
`format`, the write causes the contents of the image’s memory to become
**undefined**.

If the `Sampled` `Type` of the `OpTypeImage` does not match the
[SPIR-V Type](../appendices/spirvenv.html#spirv-type), the write causes the value of the texel to
become **undefined**.
For integer types, if the [signedness of the access](../appendices/spirvenv.html#spirvenv-image-signedness) does not match the signedness of the accessed resource, the write
causes the value of the texel to become **undefined**.

The integer texel coordinates are validated according to the same rules as
for texel input [coordinate validation](#textures-integer-coordinate-validation).

If the texel fails integer texel coordinate validation, then the write has
no effect.

If the texel attempts to write to an unbound region of a sparse image, the
texel is a sparse unbound texel.
In such a case, if the
[VkPhysicalDeviceSparseProperties](sparsemem.html#VkPhysicalDeviceSparseProperties)::`residencyNonResidentStrict`
property is `VK_TRUE`, the sparse unbound texel write has no effect.
If `residencyNonResidentStrict` is `VK_FALSE`, the write **may** have a
side effect that becomes visible to other accesses to unbound texels in any
resource, but will not be visible to any device memory allocated by the
application.

If the image format is sRGB, a linear to sRGB conversion is applied to the
R, G, and B components as described in the “sRGB EOTF” section of the
[Khronos Data Format Specification](introduction.html#data-format).
The A component, if present, is unchanged.

Texels then undergo a format conversion from the floating-point, signed, or
unsigned integer type of the texel data to the [VkFormat](formats.html#VkFormat) of the image
view.
If the number of components in the texel data is larger than the number of
components in the format, additional components are discarded.

Each component is converted based on its type and size (as defined in the
[Format Definition](formats.html#formats-definition) section for each [VkFormat](formats.html#VkFormat)).
Floating-point outputs are converted as described in
[Floating-Point Format Conversions](fundamentals.html#fundamentals-fp-conversion) and
[Fixed-Point Data Conversion](fundamentals.html#fundamentals-fixedconv).
Integer outputs are converted such that their value is preserved.
The converted value of any integer that cannot be represented in the target
format is **undefined**.

If the `VkImageView` format has an X component in its format
description, **undefined** values are written to those bits.

If the underlying `VkImage` format has an X component in its format
description, **undefined** values are also written to those bits, even if
result format conversion produces a valid value for those bits because the
`VkImageView` format is different.

If the image sampler instruction provides normalized texel coordinates, some
of the following operations are performed.

For `Proj` image operations, the normalized texel coordinates
(s,t,r,q,a) and (if present) the Dref coordinate are
transformed as follows:

  

  

Derivatives are used for LOD selection.
These derivatives are either implicit (in an `ImplicitLod` image
instruction in a
mesh, task,
compute, or
fragment shader) or explicit (provided explicitly by shader to the image
instruction in any shader).

For implicit derivatives image instructions, the derivatives of texel
coordinates are calculated in the same manner as
[derivative operations](shaders.html#shaders-derivative-operations).
That is:

  

  

Partial derivatives not defined above for certain image dimensionalities are
set to zero.

For explicit LOD image instructions, if the **optional** SPIR-V operand
`Grad` is provided, then the operand values are used for the derivatives.
The number of components present in each derivative for a given image
dimensionality matches the number of partial derivatives computed above.

If the **optional** SPIR-V operand `Lod` is provided, then derivatives are
set to zero, the cube map derivative transformation is skipped, and the
scale factor operation is skipped.
Instead, the floating-point scalar coordinate is directly assigned to
λbase as described in [LOD Operation](#textures-level-of-detail-operation).

If the image or sampler object used by an implicit derivative image
instruction is not uniform across the quad and
[`quadDivergentImplicitLod`](devsandqueues.html#limits-quadDivergentImplicitLod) is not
supported, then the derivative and LOD values are **undefined**.
Implicit derivatives are well-defined when the image and sampler and control
flow are uniform across the quad, even if they diverge between different
quads.

If [`quadDivergentImplicitLod`](devsandqueues.html#limits-quadDivergentImplicitLod) is
supported, then derivatives and implicit LOD values are well-defined even if
the image or sampler object are not uniform within a quad.
The derivatives are computed as specified above, and the implicit LOD
calculation proceeds for each shader invocation using its respective image
and sampler object.

For cube map image instructions, the (s,t,r) coordinates are treated
as a direction vector (rx,ry,rz).
The direction vector is used to select a cube map face.
The direction vector is transformed to a per-face texel coordinate system
(sface,tface), The direction vector is also used to transform the
derivatives to per-face derivatives.

The direction vector selects one of the cube map’s faces based on the
largest magnitude coordinate direction (the major axis direction).
Since two or more coordinates **can** have identical magnitude, the
implementation **must** have rules to disambiguate this situation.

The rules **should** have as the first rule that rz wins over
ry and rx, and the second rule that ry wins over
rx.
An implementation **may** choose other rules, but the rules **must** be
deterministic and depend only on (rx,ry,rz).

The layer number (corresponding to a cube map face), the coordinate
selections for sc, tc, rc, and the selection of
derivatives, are determined by the major axis direction as specified in the
following two tables.

Table 4. Cube Map Face and Coordinate Selection

Major Axis Direction
Layer Number
Cube Map Face
sc
tc
rc

+rx
0
Positive X
-rz
-ry
rx

-rx
1
Negative X
+rz
-ry
rx

+ry
2
Positive Y
+rx
+rz
ry

-ry
3
Negative Y
+rx
-rz
ry

+rz
4
Positive Z
+rx
-ry
rz

-rz
5
Negative Z
-rx
-ry
rz

Table 5. Cube Map Derivative Selection

Major Axis Direction
∂sc / ∂x
∂sc / ∂y
∂tc / ∂x
∂tc / ∂y
∂rc / ∂x
∂rc / ∂y

+rx
-∂rz / ∂x
-∂rz / ∂y
-∂ry / ∂x
-∂ry / ∂y
+∂rx / ∂x
+∂rx / ∂y

-rx
+∂rz / ∂x
+∂rz / ∂y
-∂ry / ∂x
-∂ry / ∂y
-∂rx / ∂x
-∂rx / ∂y

+ry
+∂rx / ∂x
+∂rx / ∂y
+∂rz / ∂x
+∂rz / ∂y
+∂ry / ∂x
+∂ry / ∂y

-ry
+∂rx / ∂x
+∂rx / ∂y
-∂rz / ∂x
-∂rz / ∂y
-∂ry / ∂x
-∂ry / ∂y

+rz
+∂rx / ∂x
+∂rx / ∂y
-∂ry / ∂x
-∂ry / ∂y
+∂rz / ∂x
+∂rz / ∂y

-rz
-∂rx / ∂x
-∂rx / ∂y
-∂ry / ∂x
-∂ry / ∂y
-∂rz / ∂x
-∂rz / ∂y

  

  

The partial derivatives of the [Cube Map Coordinate Transformations](#textures-cube-map-coordinate-transform) can be computed as:

  

  

The other derivatives are simplified similarly, resulting in

  

  

LOD selection **can** be either explicit (provided explicitly by the image
instruction) or implicit (determined from a scale factor calculated from the
derivatives).
The LOD **must** be computed with `mipmapPrecisionBits` of accuracy.

The magnitude of the derivatives are calculated by:

mux = |∂s/∂x| × wbase

mvx = |∂t/∂x| × hbase

mwx = |∂r/∂x| × dbase

muy = |∂s/∂y| × wbase

mvy = |∂t/∂y| × hbase

mwy = |∂r/∂y| × dbase

where:

∂t/∂x = ∂t/∂y = 0 (for 1D
images)

∂r/∂x = ∂r/∂y = 0 (for 1D,
2D or Cube images)

and:

wbase = image.w

hbase = image.h

dbase = image.d

(for the `baseMipLevel`, from the image descriptor).

For corner-sampled images, the wbase, hbase, and
dbase are instead:

wbase = image.w - 1

hbase = image.h - 1

dbase = image.d - 1

A point sampled in screen space has an elliptical footprint in texture
space.
The minimum and maximum scale factors (ρmin, ρmax) **should**
be the minor and major axes of this ellipse.

The *scale factors* ρx and ρy, calculated from the
magnitude of the derivatives in x and y, are used to compute the minimum and
maximum scale factors.

ρx and ρy **may** be approximated with functions
fx and fy, subject to the following constraints:

  

  

  

  

The minimum and maximum scale factors (ρmin,ρmax) are
determined by:

ρmax = max(ρx, ρy)

ρmin = min(ρx, ρy)

The ratio of anisotropy is determined by:

η = min(ρmax/ρmin, maxAniso)

where:

sampler.maxAniso = `maxAnisotropy` (from sampler
descriptor)

limits.maxAniso = `maxSamplerAnisotropy` (from
physical device limits)

maxAniso = min(sampler.maxAniso, limits.maxAniso)

If ρmax = ρmin = 0, then all the partial derivatives are
zero, the fragment’s footprint in texel space is a point, and η
**should** be treated as 1.
If ρmax ≠ 0 and ρmin = 0 then all partial
derivatives along one axis are zero, the fragment’s footprint in texel space
is a line segment, and η **should** be treated as maxAniso.
However, anytime the footprint is small in texel space the implementation
**may** use a smaller value of η, even when ρmin is zero
or close to zero.
If either [VkPhysicalDeviceFeatures](features.html#VkPhysicalDeviceFeatures)::`samplerAnisotropy` or
[VkSamplerCreateInfo](samplers.html#VkSamplerCreateInfo)::`anisotropyEnable` are `VK_FALSE`,
maxAniso is set to 1.

If η = 1, sampling is isotropic.
If η > 1, sampling is anisotropic.

The sampling rate (N) is derived as:

N = ⌈η⌉

An implementation **may** round N up to the nearest supported sampling
rate.
An implementation **may** use the value of N as an approximation of
η.

The LOD parameter λ is computed as follows:

  

  

where:

  

  

and maxSamplerLodBias is the value of the [VkPhysicalDeviceLimits](limits.html#VkPhysicalDeviceLimits)
feature [`maxSamplerLodBias`](limits.html#limits-maxSamplerLodBias).

The image level(s) d, dhi, and dlo which texels are
read from are determined by an image-level parameter dl, which is
computed based on the LOD parameter, as follows:

  

  

where:

  

  

  

  

and:

  

  

`baseMipLevel` and `levelCount` are taken from the
`subresourceRange` of the image view.

minLodimageView **must** be less or equal to levelbase + q.

If the sampler’s `mipmapMode` is `VK_SAMPLER_MIPMAP_MODE_NEAREST`,
then the level selected is d = dl.

If the sampler’s `mipmapMode` is `VK_SAMPLER_MIPMAP_MODE_LINEAR`,
two neighboring levels are selected:

  

  

δ is the fractional value, quantized to the number of
[mipmap precision bits](limits.html#limits-mipmapPrecisionBits), used for
[linear filtering](#textures-texel-filtering) between levels.

The normalized texel coordinates are scaled by the image level dimensions
and the array layer is selected.

This transformation is performed once for each level used in
[filtering](#textures-texel-filtering) (either d, or dhi and
dlo).

  

  

where:

widthscale = widthlevel

heightscale = heightlevel

depthscale = depthlevel

for conventional images, and:

widthscale = widthlevel - 1

heightscale = heightlevel - 1

depthscale = depthlevel - 1

for corner-sampled images.

and where (Δi, Δj, Δk) are
taken from the image instruction if it includes a `ConstOffset` or
`Offset` operand, otherwise they are taken to be zero.

Operations then proceed to Unnormalized Texel Coordinate Operations.

The unnormalized texel coordinates are transformed to integer texel
coordinates relative to the selected mipmap level.

The layer index l is computed as:

l = clamp(RNE(a), 0, `layerCount` - 1) + 
`baseArrayLayer`

where `layerCount` is the number of layers in the image subresource
range of the image view, `baseArrayLayer` is the first layer from the
subresource range, and where:

  

  

The sample index n is assigned the value 0.

Nearest filtering (`VK_FILTER_NEAREST`) computes the integer texel
coordinates that the unnormalized coordinates lie within:

  

  

where:

shift = 0.0

for conventional images, and:

shift = 0.5

for corner-sampled images.

Linear filtering (`VK_FILTER_LINEAR`) computes a set of neighboring
coordinates which bound the unnormalized coordinates.
The integer texel coordinates are combinations of i0 or i1,
j0 or j1, k0 or k1, as well as weights
α, β, and γ.

  

  

  

  

where:

shift = 0.5

for conventional images, and:

shift = 0.0

for corner-sampled images,
and where:

  

  

where the number of fraction bits retained is specified by
`VkPhysicalDeviceLimits`::`subTexelPrecisionBits`.

Cubic filtering (`VK_FILTER_CUBIC_EXT`) computes a set of neighboring
coordinates which bound the unnormalized coordinates.
The integer texel coordinates are combinations of i0, i1,
i2 or i3, j0, j1, j2 or j3,
k0, k1, k2 or k3, as well as weights
α, β, and γ.

  

  

  

  

where:

  

  

where the number of fraction bits retained is specified by
`VkPhysicalDeviceLimits`::`subTexelPrecisionBits`.

Integer texel coordinate operations **may** supply a LOD which texels are to be
read from or written to using the optional SPIR-V operand `Lod`.
If the `Lod` is provided then it **must** be an integer.

The image level selected is:

  

  

If d does not lie in the range [`baseMipLevel`,
`baseMipLevel` +  `levelCount`)
or d is less than minLodIntegerimageView,
then any values fetched are
zero if the [`robustImageAccess2`](features.html#features-robustImageAccess2)
feature is enabled, otherwise are
**undefined**, and any writes (if supported) are discarded.

If the used sampler was created without
`VK_SAMPLER_CREATE_NON_SEAMLESS_CUBE_MAP_BIT_EXT`,
`Cube` images ignore the wrap modes specified in the sampler.
Instead, if `VK_FILTER_NEAREST` is used within a mip level then
`VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_EDGE` is used, and if
`VK_FILTER_LINEAR` is used within a mip level then sampling at the edges
is performed as described earlier in the [Cube map edge handling](#textures-cubemapedge) section.

The first integer texel coordinate i is transformed based on the
`addressModeU` parameter of the sampler.

  

  

where:

  

  

j (for 2D and Cube image) and k (for 3D image) are similarly
transformed based on the `addressModeV` and `addressModeW`
parameters of the sampler, respectively.

SPIR-V instructions with `Gather` in the name return a vector derived
from 4 texels in the base level of the image view.
The rules for the `VK_FILTER_LINEAR` minification filter are applied to
identify the four selected texels.
Each texel is then converted to an RGBA value according to
[conversion to RGBA](#textures-conversion-to-rgba) and then
[swizzled](#textures-component-swizzle).
A four-component vector is then assembled by taking the component indicated
by the `Component` value in the instruction from the swizzled color value
of the four texels.
If the operation does not use the `ConstOffsets` image operand then the
four texels form the 2 × 2 rectangle used for texture filtering:

  

  

If the operation does use the `ConstOffsets` image operand then the
offsets allow a custom filter to be defined:

  

  

where:

  

  

`OpImage*Gather` **must** not be used on a sampled image with
[sampler Y′CBCR conversion](samplers.html#samplers-YCbCr-conversion) enabled.

If levelbase imageView, then any values fetched are
zero if the [`robustImageAccess2`](features.html#features-robustImageAccess2)
feature is enabled.
Otherwise values are
**undefined**.

Texel filtering is first performed for each level (either d or
dhi and dlo).

If λ is less than or equal to zero, the texture is said to be
*magnified*, and the filter mode within a mip level is selected by the
`magFilter` in the sampler.
If λ is greater than zero, the texture is said to be
*minified*, and the filter mode within a mip level is selected by the
`minFilter` in the sampler.

Within a mip level, `VK_FILTER_NEAREST` filtering selects a single value
using the (i, j, k) texel coordinates, with all texels taken from
layer l.

  

  

Within a mip level, `VK_FILTER_LINEAR` filtering combines 8 (for 3D), 4
(for 2D or Cube), or 2 (for 1D) texel values, together with their linear
weights.
The linear weights are derived from the fractions computed earlier:

  

  

The values of multiple texels, together with their weights, are combined to
produce a filtered value.

The [VkSamplerReductionModeCreateInfo](samplers.html#VkSamplerReductionModeCreateInfo)::`reductionMode` **can** control
the process by which multiple texels, together with their weights, are
combined to produce a filtered texture value.

When the `reductionMode` is set (explicitly or implicitly) to
`VK_SAMPLER_REDUCTION_MODE_WEIGHTED_AVERAGE`, a weighted average is
computed:

  

  

However, if the reduction mode is `VK_SAMPLER_REDUCTION_MODE_MIN` or
`VK_SAMPLER_REDUCTION_MODE_MAX`, the process operates on the above set
of multiple texels, together with their weights, computing a component-wise
minimum or maximum, respectively, of the components of the set of texels
with non-zero weights.

Within a mip level, `VK_FILTER_CUBIC_EXT`, filtering computes a weighted
average of
64 (for 3D),
16 (for 2D), or 4 (for 1D) texel values, together with their
Catmull-Rom, Zero Tangent Cardinal, B-Spline, or Mitchell-Netravali weights
as specified by [VkSamplerCubicWeightsCreateInfoQCOM](samplers.html#VkSamplerCubicWeightsCreateInfoQCOM).

Catmull-Rom weights
specified by `VK_CUBIC_FILTER_WEIGHTS_CATMULL_ROM_QCOM`
are derived from the fractions computed earlier.

  

  

Zero Tangent Cardinal weights specified by
`VK_CUBIC_FILTER_WEIGHTS_ZERO_TANGENT_CARDINAL_QCOM` are derived from
the fractions computed earlier.

  

  

B-Spline weights specified by `VK_CUBIC_FILTER_WEIGHTS_B_SPLINE_QCOM`
are derived from the fractions computed earlier.

  

  

Mitchell-Netravali weights specified by
`VK_CUBIC_FILTER_WEIGHTS_MITCHELL_NETRAVALI_QCOM` are derived from the
fractions computed earlier.

  

  

The values of multiple texels, together with their weights, are combined to
produce a filtered value.

The [VkSamplerReductionModeCreateInfo](samplers.html#VkSamplerReductionModeCreateInfo)::`reductionMode` **can** control
the process by which multiple texels, together with their weights, are
combined to produce a filtered texture value.

When the `reductionMode` is set (explicitly or implicitly) to
`VK_SAMPLER_REDUCTION_MODE_WEIGHTED_AVERAGE`
or `VK_SAMPLER_REDUCTION_MODE_WEIGHTED_AVERAGE_RANGECLAMP_QCOM`
, a weighted average is computed:

  

  

However, if the reduction mode is `VK_SAMPLER_REDUCTION_MODE_MIN` or
`VK_SAMPLER_REDUCTION_MODE_MAX`, the process operates on the above set
of multiple texels, together with their weights, computing a component-wise
minimum or maximum, respectively, of the components of the set of texels
with non-zero weights.

When `reductionMode` is
`VK_SAMPLER_REDUCTION_MODE_WEIGHTED_AVERAGE_RANGECLAMP_QCOM`, the
weighted average is clamped to be within the component-wise minimum and
maximum of the set of texels with non-zero weights.

`VK_SAMPLER_MIPMAP_MODE_NEAREST` filtering returns the value of a single
mipmap level,

τ = τ[d].

`VK_SAMPLER_MIPMAP_MODE_LINEAR` filtering combines the values of
multiple mipmap levels (τ[hi] and τ[lo]), together with their linear
weights.

The linear weights are derived from the fraction computed earlier:

  

  

The values of multiple mipmap levels, together with their weights, are
combined to produce a final filtered value.

The [VkSamplerReductionModeCreateInfo](samplers.html#VkSamplerReductionModeCreateInfo)::`reductionMode` **can** control
the process by which multiple texels, together with their weights, are
combined to produce a filtered texture value.

When the `reductionMode` is set (explicitly or implicitly) to
`VK_SAMPLER_REDUCTION_MODE_WEIGHTED_AVERAGE`, a weighted average is
computed:

  

  

However, if the reduction mode is `VK_SAMPLER_REDUCTION_MODE_MIN` or
`VK_SAMPLER_REDUCTION_MODE_MAX`, the process operates on the above
values, together with their weights, computing a component-wise minimum or
maximum, respectively, of the components of the values with non-zero
weights.

Anisotropic filtering is enabled by the `anisotropyEnable` in the
sampler.
When enabled, the image filtering scheme accounts for a degree of
anisotropy.

The particular scheme for anisotropic texture filtering is
implementation-dependent.
Implementations **should** consider the `magFilter`, `minFilter` and
`mipmapMode` of the sampler to control the specifics of the anisotropic
filtering scheme used.
In addition, implementations **should** consider `minLod` and `maxLod`
of the sampler.

The SPIR-V instruction `OpImageSampleFootprintNV` evaluates the set of
texels from a single mip level that would be accessed during a
[texel filtering](#textures-texel-filtering) operation.
In addition to the inputs that would be accepted by an equivalent
`OpImageSample*` instruction, `OpImageSampleFootprintNV` accepts two
additional inputs.
The `Granularity` input is an integer identifying the size of texel
groups used to evaluate the footprint.
Each bit in the returned footprint mask corresponds to an aligned block of
texels whose size is given by the following table:

Table 6. Texel Footprint Granularity Values

`Granularity`
`Dim` = 2D
`Dim` = 3D

0
unsupported
unsupported

1
2x2
2x2x2

2
4x2
unsupported

3
4x4
4x4x2

4
8x4
unsupported

5
8x8
unsupported

6
16x8
unsupported

7
16x16
unsupported

8
unsupported
unsupported

9
unsupported
unsupported

10
unsupported
16x16x16

11
64x64
32x16x16

12
128x64
32x32x16

13
128x128
32x32x32

14
256x128
64x32x32

15
256x256
unsupported

The `Coarse` input is used to select between the two mip levels that **may**
be accessed during texel filtering when using a `mipmapMode` of
`VK_SAMPLER_MIPMAP_MODE_LINEAR`.
When filtering between two mip levels, a `Coarse` value of `true`
requests the footprint in the lower-resolution mip level (higher level
number), while `false` requests the footprint in the higher-resolution
mip level.
If texel filtering would access only a single mip level, the footprint in
that level would be returned when `Coarse` is `false`; an empty
footprint would be returned when `Coarse` is `true`.

The footprint for `OpImageSampleFootprintNV` is returned in a structure
with six members:

* 
The first member is a boolean value that is true if the texel filtering
operation would access only a single mip level.

* 
The second member is a two- or three-component integer vector holding
the footprint anchor location.
For two-dimensional images, the returned components are in units of
eight texel groups.
For three-dimensional images, the returned components are in units of
four texel groups.

* 
The third member is a two- or three-component integer vector holding a
footprint offset relative to the anchor.
All returned components are in units of texel groups.

* 
The fourth member is a two-component integer vector mask, which holds a
bitfield identifying the set of texel groups in an 8x8 or 4x4x4
neighborhood relative to the anchor and offset.

* 
The fifth member is an integer identifying the mip level containing the
footprint identified by the anchor, offset, and mask.

* 
The sixth member is an integer identifying the granularity of the
returned footprint.

For footprints in two-dimensional images (`Dim2D`), the mask returned by
`OpImageSampleFootprintNV` indicates whether each texel group in a 8x8
local neighborhood of texel groups would have one or more texels accessed
during texel filtering.
In the mask, the texel group with local group coordinates
   is considered covered if and only if

  

  

where:

* 
   and   ; and

* 
   is the returned two-component mask.

The local group with coordinates    in the mask is
considered covered if and only if the texel filtering operation would access
one or more texels    in the returned mip level where:

  

  

and

* 
   and   ;

* 
   is a two-component vector holding the width and height
of the texel group identified by the granularity;

* 
   is the returned two-component anchor vector; and

* 
   is the returned two-component offset vector.

For footprints in three-dimensional images (`Dim3D`), the mask returned
by `OpImageSampleFootprintNV` indicates whether each texel group in a
4x4x4 local neighborhood of texel groups would have one or more texels
accessed during texel filtering.
In the mask, the texel group with local group coordinates
  , is considered covered if and only if:

  

  

where:

* 
  ,   , and \(0
\leq lgz    is the returned two-component mask.

The local group with coordinates    in the mask is
considered covered if and only if the texel filtering operation would access
one or more texels    in the returned mip level where:

  

  

and

* 
  ,   ,
  ;

* 
   is a three-component vector holding the width, height,
and depth of the texel group identified by the granularity;

* 
   is the returned three-component anchor vector; and

* 
   is the returned three-component offset vector.

If the sampler used by `OpImageSampleFootprintNV` enables anisotropic
texel filtering via `anisotropyEnable`, it is possible that the set of
texel groups accessed in a mip level may be too large to be expressed using
an 8x8 or 4x4x4 mask using the granularity requested in the instruction.
In this case, the implementation uses a texel group larger than the
requested granularity.
When a larger texel group size is used, `OpImageSampleFootprintNV`
returns an integer granularity value that **can** be interpreted in the same
manner as the granularity value provided to the instruction to determine the
texel group size used.
If anisotropic texel filtering is disabled in the sampler, or if an
anisotropic footprint can be represented as an 8x8 or 4x4x4 mask with the
requested granularity, `OpImageSampleFootprintNV` will use the requested
granularity as-is and return a granularity value of zero.

`OpImageSampleFootprintNV` supports only two- and three-dimensional image
accesses (`Dim2D` and `Dim3D`), and the footprint returned is
**undefined** if a sampler uses an addressing mode other than
`VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_EDGE`.

The SPIR-V instruction `OpImageWeightedSampleQCOM` specifies a texture
sampling operation involving two images: the *sampled image* and the *weight
image*.
It is similar to bilinear filtering except more than 2x2 texels may
participate in the filter and the filter weights are application-specified
rather than computed by fixed-function hardware.
The weight image view defines a 2D kernel weights used during sampling.

The `OpImageWeightedSampleQCOM` support normalized or unnormalized texel
coordinates.
In addition to the inputs that would be accepted by an equivalent
`OpImageSample*` instruction, `OpImageWeightedSampleQCOM` accepts a
`weight` input that specifies the view of a sample weight image

The input `weight` **must** be a view of a 2D or 1D image with
`miplevels` equal to `1`, `samples` equal to
`VK_SAMPLE_COUNT_1_BIT`, created with an identity swizzle, and created
with `usage` that includes `VK_IMAGE_USAGE_SAMPLE_WEIGHT_BIT_QCOM`.
The [VkImageViewSampleWeightCreateInfoQCOM](resources.html#VkImageViewSampleWeightCreateInfoQCOM) specifies additional
parameters of the view: `filterCenter`, `filterSize`, and
`numPhases`.
described in more detail below.

The `weight` input **must** be bound using a
[sample weight image](descriptorsets.html#descriptorsets-weightimage) descriptor type.
The `weight` view defines a filtering kernel that is a region of view’s
subresource range.
The kernel spans a region from integer texel coordinate (0,0) to
(`filterSize.x`-1, `filterSize.y`-1).
It is valid for the view’s subresource to have dimensions larger than the
kernel but the texels with integer coordinates greater than
(`filterSize.width`-1, `filterSize.height`-1) are ignored by
weight sampling.
The value returned by queries `OpImageQuerySize`,
`OpImageQuerySizeLod`, `OpImageQueryLevels`, and
`OpImageQuerySamples` return for a weight image is **undefined**.

`filterCenter` designates an integer texel coordinate within the filter
kernel as being the 'center' of the kernel.
The center **must** be in the range (0,0) to (`filterSize.x`-1,
`filterSize.y`-1).
`numPhases` describes the number of filter phases used to provide
sub-pixel filtering.
Both are described in more detail below.

The weight image specifies filtering kernel weight values.
A 2D image view can be used to specify a 2D matrix of filter weights.
For separable filers, a 1D image view can be used to specity the horizontal
and vertical weights.

A 2D image view defined with [VkImageViewSampleWeightCreateInfoQCOM](resources.html#VkImageViewSampleWeightCreateInfoQCOM)
describes a 2D matrix (`filterSize.width` ×
`filterSize.height`) of weight elements with filter’s center point at
`filterCenter`.
Note that `filterSize` can be smaller than the view’s subresource, but
the filter will always be located starting at integer texel coordinate
(0,0).

The following figure illustrates a 2D convolution filter having
`filterSize` of (4,3) and `filterCenter` at (1, 1).

![weight filter 2d](../_images/weight_filter_2d.svg)

Figure 10. 2D Convolution Filter

For a 2D weight filter, the phases are stored as layers of a 2D array image.
The width and height of the view’s subresource range **must** be less than or
equal to
[VkPhysicalDeviceImageProcessingPropertiesQCOM](devsandqueues.html#VkPhysicalDeviceImageProcessingPropertiesQCOM)::`maxWeightFilterDimension`.
The layers are stored in horizontal phase major order.
Expressed as a formula, the layer index for each filter phase is computed
as:

layerIndex(horizPhase,vertPhase,horizPhaseCount) = (vertPhase * horizPhaseCount) + horizPhase

A separable weight filter is a 2D filter that can be specified by two 1D
filters in the x and y directions such that their product yields
the 2D filter.
The following example shows a 2D filter and its associated separable 1D
horizontal and vertical filters.

![weight filter 1d separable](../_images/weight_filter_1d_separable.svg)

Figure 11. Separable 2D Convolution Filter

A 1D array image view defined with
[VkImageViewSampleWeightCreateInfoQCOM](resources.html#VkImageViewSampleWeightCreateInfoQCOM) and with `layerCount` equal
to '2' describes a separable weight filter.
The horizontal weights are specified in slice '0' and the vertical weights
in slice '1'.
The `filterSize` and `filterCenter` specify the size and origin of
the of the horizontal and vertical filters.
For many use cases, 1D separable filters can offer a performance advantage
over 2D filters.

For a 1D separable weight filter, the phases are arranged into a 1D array
image with two layers.
The horizontal weights are stored in layer 0 and the vertical weights in
layer 1.
Within each layer of the 1D array image, the weights are arranged into
groups of 4, and then arranged by phase.
Expressed as a formula, the 1D texel offset for each weight within each
layer is computed as:

// Let horizontal weights have a weightIndex of [0, filterSize.width - 1]
// Let vertical weights have a weightIndex of [0, filterSize.height - 1]
// Let phaseCount be the number of phases in either the vertical or horizontal direction.

texelOffset(phaseIndex,weightIndex,phaseCount) = (phaseCount * 4 * (weightIndex / 4)) + (phaseIndex * 4) + (weightIndex % 4)

When using weight image sampling, the texture coordinates may not align with
a texel center in the sampled image.
In this case, the filter weights can be adjusted based on the subpixel
location.
This is termed “subpixel filtering” to indicate that the origin of the
filter lies at a subpixel location other than the texel center.
Conceptually, this means that the weight filter is positioned such that
filter taps do not align with sampled texels exactly.
In such a case, modified filter weights may be needed to adjust for the
off-center filter taps.
Unlike bilinear filtering where the subpixel weights are computed by the
implementation, subpixel weight image sampling requires that the per-phase
filter weights are pre-computed by the application and stored in an array
where each slice of the array is a “filter phase”.
The array is indexed by the implementation based on subpixel positioning.
Rather than a single 2D kernel of filter weights, the application provides
an array of kernels, one set of filter weights per phase.

The number of phases are restricted by following requirements, which apply
to both separable and non-separable filters:

* 
The number of phases in the vertical direction, phaseCountvert,
**must** be a power of two (i.e., 1, 2, 4, etc.).

* 
The number of phases in the horizontal direction
phaseCounthoriz, **must** equal phaseCountvert.

* 
The total number of phases, phaseCountvert ×
phaseCounthoriz, **must** be less than or equal to
[VkPhysicalDeviceImageProcessingPropertiesQCOM](devsandqueues.html#VkPhysicalDeviceImageProcessingPropertiesQCOM)::`maxWeightFilterPhases`.

Weight sampling requires `VkSamplerCreateInfo` `addressModeU` and
`addressModeV` **must** be `VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_EDGE` or
`VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_BORDER`.
If `VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_BORDER` is used, then the border
color **must** be `VK_BORDER_COLOR_FLOAT_TRANSPARENT_BLACK`.

The 2D unnormalized texel coordinates    are transformed by
   to specify coordinates   .

  

  

where    is specified by
[VkImageViewSampleWeightCreateInfoQCOM](resources.html#VkImageViewSampleWeightCreateInfoQCOM)::`filterCenter`.

Two sets of neighboring integer 2D texel coordinates are generated.
The first set is used for selecting texels from the sampled image
   and the second set used for selecting texels from the
weight image   .
The first set of neighboring coordinates are combinations of
   to    and    to
  .
The second set of neighboring coordinates are combinations of
   to    and    to
  .
The first and second sets each contain \((filterWidth \times
filterHeight)\) of pairs of    and   
coordinates respectively.

  

  

where    and    are specified by
[VkImageViewSampleWeightCreateInfoQCOM](resources.html#VkImageViewSampleWeightCreateInfoQCOM)::`filterSize`.

Each of the generated integer coordinates    is
transformed by [texture wrapping operation](#textures-wrapping-operation),
followed by [integer texel coordinate validation](#textures-integer-coordinate-validation), If any coordinate fails coordinate validation, it
is a Border Texel and [texel replacement](#textures-texel-replacement) is
performed.

The phase index    is computed from the fraction bits of the
unnormalized 2D texel coordinates:

  

  

where the number of fraction bits retained is
   specified by
[VkImageViewSampleWeightCreateInfoQCOM](resources.html#VkImageViewSampleWeightCreateInfoQCOM)::`numPhases`

Each pair of texel coordinates    in the first set selects a
single texel value    from the sampled image.
Each pair of texel coordinates    in the second set, combined
with phaseIndex   , selects a single weight from the weight
image    .

  

  

If    is a 2D array view, then non-separable filtering is
specified, and integer coordinates    are used to select
texels from layer    of   .
If    is a 1D array view, then separable filtering is specified
and integer coordinates    are transformed to
  , and used to select horizontal weight
   and vertical weight    texels
from layer 0 and layer 1 of    respectively.

  

  

Where    refers to the integer modulo operator.

The values of multiple texels, together with their weights, are combined to
produce a filtered value.

  

  

When [VkSamplerReductionModeCreateInfo](samplers.html#VkSamplerReductionModeCreateInfo)::`reductionMode` is
`VK_SAMPLER_REDUCTION_MODE_WEIGHTED_AVERAGE`, the above summation is
used.
However, if the reduction mode is `VK_SAMPLER_REDUCTION_MODE_MIN` or
`VK_SAMPLER_REDUCTION_MODE_MAX`, the process operates on the above
values, computing a component-wise minimum or maximum of the texels with
non-zero weights.
If the reduction mode is `VK_SAMPLER_REDUCTION_MODE_MIN` or
`VK_SAMPLER_REDUCTION_MODE_MAX`, each    weight
**must** be equal to 0.0 or 1.0, otherwise the **undefined** values are returned.

Finally, the operations described in
[Conversion to RGBA](#textures-conversion-to-rgba) and
[Component swizzle](#textures-component-swizzle) are performed and the final
result is returned to the shader.

The SPIR-V instruction `opImageBlockMatchSAD` and
`opImageBlockMatchSSD` specify texture block matching operations where a
block or region of texels within a *target image* is compared with a
same-sized region a *reference image*.
The instructions make use of two image views: the *target view* and the
*reference view*.
The target view and reference view can be the same view, allowing block
matching of two blocks within a single image.

Similar to an equivalent `OpImageFetch` instruction,
`opImageBlockMatchSAD` and `opImageBlockMatchSAD` specify an
`image` and an integer texel `coordinate` which describes the
bottom-left texel of the target block.
There are three additional inputs.
The `reference` and `refCoodinate` specifies bottom-left texel of the
reference block.
The `blockSize` specifies the integer width and height of the target and
reference blocks to be compared, and **must** not be greater than
[VkPhysicalDeviceImageProcessingPropertiesQCOM](devsandqueues.html#VkPhysicalDeviceImageProcessingPropertiesQCOM).`maxBlockMatchRegion`.

`opImageBlockMatchWindowSAD` and `opImageBlockMatchWindowSAD` take the
same input parameters as the corresponding non-window instructions.
The block matching comparison is performed for all pixel values within a 2D
window whose dimensions are specified in the sampler.

For `opImageBlockMatchSAD` and `opImageBlockMatchSSD`, the input
`sampler` **must** be created with `addressModeU` and `addressModeV`,
equal to `VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_EDGE`, or
`VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_BORDER` with
`VK_BORDER_COLOR_FLOAT_TRANSPARENT_BLACK`.
The input `sampler` **must** be created with `unnormalizedCoordinates`
equal to `VK_TRUE`.
The input `sampler` **must** be created with `components` equal to
`VK_COMPONENT_SWIZZLE_IDENTITY`.

For `opImageBlockMatchWindowSAD` and `opImageBlockMatchWindowSSD`
instructions, the `target` sampler **must** have been created with
[VkSamplerBlockMatchWindowCreateInfoQCOM](samplers.html#VkSamplerBlockMatchWindowCreateInfoQCOM) in the `pNext` chain.

For `opImageBlockMatchWindowSAD`, `opImageBlockMatchWindowSSD`,
`opImageBlockMatchGatherSAD`, or
`opImageBlockMatchGatherSSDinstructions`, the input `sampler` **must** be
created with `addressModeU` and `addressModeV`, equal to
`VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_BORDER` with
`VK_BORDER_COLOR_FLOAT_TRANSPARENT_BLACK`.

Other sampler states are ignored.

Block matching SPIR-V instructions `opImageBlockMatchSAD` and
`opImageBlockMatchSSD` specify two sets of 2D integer texel coordinates:
target coordinates    and reference coordinates
  .

The coordinates define the bottom-left texel of the target block
   and the reference block \((k_{0},
l_{0})\).

  

  

For the target block, a set of neighboring integer texel coordinates are
generated.
The neighboring coordinates are combinations of    to
   and    to
  .
The set is of size   .

  

  

where    and    is specified by the
`blockSize` operand.

If any target integer texel coordinate    in the set fails
[integer texel coordinate validation](#textures-integer-coordinate-validation), then the texel is an invalid texel and
[texel replacement](#textures-texel-replacement) is performed.

Similarly for the reference block, a set of neighboring integer texel
coordinates are generated.

  

  

Each reference texel coordinate    in the set **must** not fail
[integer texel coordinate validation](#textures-integer-coordinate-validation).
To avoid **undefined** behavior, application shader should guarantee that the
reference block is fully within the bounds of the reference image.

Each pair of texel coordinates    in the set selects a single
texel value from the target image   .
Each pair of texel coordinates    in the set selects a single
texel value from the reference image   .

The difference between target and reference texel values is summed to
compute a difference metric.
The `opTextureBlockMatchSAD` computes the sum of absolute differences.

  

  

The `opImageBlockMatchSSD` computes the sum of the squared differences.

  

  

When [VkSamplerReductionModeCreateInfo](samplers.html#VkSamplerReductionModeCreateInfo)::`reductionMode` is
`VK_SAMPLER_REDUCTION_MODE_WEIGHTED_AVERAGE`, the above summation is
used.
However, if the reduction mode is `VK_SAMPLER_REDUCTION_MODE_MIN` or
`VK_SAMPLER_REDUCTION_MODE_MAX`, the process operates on the above
values, computing a component-wise minimum or maximum of
  , respectively.
For   , the minimum or maximum difference is computed
and for   , the square of the minimum or maximum is
computed.

Finally, the operations described in
[Conversion to RGBA](#textures-conversion-to-rgba) and
[Component swizzle](#textures-component-swizzle) are performed and the final
result is returned to the shader.
The component swizzle is specified by the *target image* descriptor; any
swizzle specified by the *reference image* descriptor is ignored.

Window block matching SPIR-V instructions `opImageBlockMatchWindowSAD`
and `opImageBlockMatchWindowSSD` specify two sets of 2D integer texel
coordinates: target coordinates    and reference coordinates
  .
The [block matching operation](#textures-blockmatch-filteroperation) is
performed repeatedly, for multiple sets of target integer coordinates within
the specified window.
These instructions effectively search a region or “window” within the
target texture and identify the window coordinates where the minimum or
maximum error metric is found.
These instructions only support single component image formats.

The target coordinates are combinations of coordinates from
   to   
where    and    are specified by
[VkSamplerBlockMatchWindowCreateInfoQCOM](samplers.html#VkSamplerBlockMatchWindowCreateInfoQCOM)::`windowExtent`.
At each target coordinate, a [block matching operation](#textures-blockmatch-filteroperation) is performed, resulting in a difference metric.
The reference coordinate    is fixed.
The block matching operation is repeated \(windowWidth \times
windowHeight\) times.

The resulting minimum or maximum error is returned in the R component of the
output.
The integer window coordinates    are returned in the G and B
components of the output.
The A component is 0.
The minimum or maximum behavior is selected by
[VkSamplerBlockMatchWindowCreateInfoQCOM](samplers.html#VkSamplerBlockMatchWindowCreateInfoQCOM)::`windowCompareMode`.

The following pseudocode describes the operation
`opImageBlockMatchWindowSAD`.
The pseudocode for `opImageBlockMatchWindowSSD` follows an identical
pattern.

vec4 opImageBlockMatchGatherSAD( sampler2D target,
                                 uvec2 targetCoord,
                                 samler2D reference,
                                 uvec2 refCoord,
                                 uvec2 blocksize) {
    // Two parameters are sourced from the VkSampler associated with
    // `target`:
    //    compareMode  (which can be either `MIN` or `MAX`)
    //    uvec2 window (which defines the search window)

    minSAD = INF;
    maxSAD = -INF;
    uvec2 minCoord;
    uvec2 maxCoord;

    for (uint x=0, x maxSAD) {
                maxSAD = SAD;
                maxCoord = uvec2(x,y);
            }
        }
    }
    if (compareMode==MIN) {
        return vec4(minSAD, minCoord.x, minCoord.y, 0.0);
    } else {
        return vec4(maxSAD, maxCoord.x, maxCoord.y, 0.0);
    }
}

Block matching Gather SPIR-V instructions `opImageBlockMatchGatherSAD`
and `opImageBlockMatchGatherSSD` specify two sets of 2D integer texel
coordinates: target coordinates    and reference coordinates
  .

These instructions perform the [block matching operation](#textures-blockmatch-filteroperation) 4 times, using integer target coordinates
  ,   ,   , and
  .
The R component from each of those 4 operations is gathered and returned in
the R, G, B, and A components of the output respectively.
For each block match operation, the reference coordinate is
  .
For each block match operation, only the R component of the target and
reference images are compared.
The following pseudocode describes the operation opImageBlockMatchGatherSAD.
The pseudocode for opImageBlockMatchGatherSSD follows an identical pattern.

vec4 opImageBlockMatchGatherSAD(sampler2D target,
                                uvec2 targetCoord,
                                samler2D reference,
                                uvec2 refCoord,
                                uvec2 blocksize) {
    vec4 out;
    for (uint x=0, x

The SPIR-V instruction `OpImageBoxFilterQCOM` specifies texture box
filtering operation where a weighted average of a region of texels is
computed, with the weights proportional to the coverage of each of the
texels.

In addition to the inputs that would be accepted by an equivalent
`OpImageSample*` instruction, `OpImageBoxFilterQCOM` accepts one
additional input, `boxSize` which specifies the width and height in
texels of the region to be averaged.

The figure below shows an example of using `OpImageBoxFilterQCOM` to
sample from a 8 × 4 texel two-dimensional image, with
unnormalized texture coordinates (4.125, 2.625) and `boxSize` of
(2.75, 2.25).
The filter will read 12 texel values and compute a weights based portion of
each texel covered by the box.

![vulkantexture boxFilter](../_images/vulkantexture_boxFilter.svg)

Figure 12. Box Filter Sampling Example

If `boxSize` has height and width both equal to 1.0, then this
instruction will behave as traditional bilinear filtering.
The `boxSize` parameter **must** be greater than or equal to 1.0 and **must**
not be greater than
[VkPhysicalDeviceImageProcessingPropertiesQCOM](devsandqueues.html#VkPhysicalDeviceImageProcessingPropertiesQCOM).`maxBoxFilterBlockSize`.

The input `sampler` **must** be created with `addressModeU` and
`addressModeV`, equal to `VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_EDGE`, or
`VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_BORDER` with
`VK_BORDER_COLOR_FLOAT_TRANSPARENT_BLACK`.

The 2D unnormalized texel coordinates    are transformed by
   to specify integer texel coordinates \((i_{0},
j_{0})\) of the bottom left texel for the filter.

  

  

where    and    are specified by the
code:(x,y) components of the `boxSize` operand.

The filter dimensions    are
computed from the fractional portion of the    coordinates
and the   .

  

  

where the number of fraction bits retained by    is
specified by `VkPhysicalDeviceLimits`::`subTexelPrecisionBits`.

A set of neighboring integer texel coordinates are generated.
The neighboring coordinates are combinations of    to
   and    to
  , with    being the
top-left coordinate of this set.
The set is of size   .

  

  

Each of the generated integer coordinates    is
transformed by [texture wrapping operation](#textures-wrapping-operation),
followed by [integer texel coordinate validation](#textures-integer-coordinate-validation), If any coordinate fails coordinate validation, it
is a Border Texel and [texel replacement](#textures-texel-replacement) is
performed.

Horizontal weights    to
   and vertical weights
   to    are
computed.
Texels that are fully covered by the box will have a horizontal and vertical
weight of 1.
Texels partially covered by the box will have will have a reduced weights
proportional to the coverage.

  

  

  

  

The values of multiple texels, together with their horizontal and vertical
weights, are combined to produce a box filtered value.

  

  

When [VkSamplerReductionModeCreateInfo](samplers.html#VkSamplerReductionModeCreateInfo)::`reductionMode` is
`VK_SAMPLER_REDUCTION_MODE_WEIGHTED_AVERAGE`, the above summation is
used.
However, if the reduction mode is `VK_SAMPLER_REDUCTION_MODE_MIN` or
`VK_SAMPLER_REDUCTION_MODE_MAX`, the process operates on the above
values, computing a component-wise minimum or maximum of the texels.

Each step described in this chapter is performed by a subset of the image
instructions:

* 
Texel Input Validation Operations, Format Conversion, Texel Replacement,
Conversion to RGBA, and Component Swizzle: Performed by all instructions
except `OpImageWrite`.

* 
Depth Comparison: Performed by `OpImage*Dref` instructions.

* 
All Texel output operations: Performed by `OpImageWrite`.

* 
Projection: Performed by all `OpImage*Proj` instructions.

* 
Derivative Image Operations, Cube Map Operations, Scale Factor
Operation, LOD Operation and Image Level(s) Selection, and Texel
Anisotropic Filtering: Performed by all `OpImageSample*` and
`OpImageSparseSample*` instructions.

* 
(s,t,r,q,a) to (u,v,w,a) Transformation, Wrapping, and (u,v,w,a) to
(i,j,k,l,n) Transformation And Array Layer Selection: Performed by all
`OpImageSample`, `OpImageSparseSample`, and `OpImage*Gather`
instructions.

* 
Texel Gathering: Performed by `OpImage*Gather` instructions.

* 
Texel Footprint Evaluation: Performed by `OpImageSampleFootprint`
instructions.

* 
Texel Filtering: Performed by all `OpImageSample*` and
`OpImageSparseSample*` instructions.

* 
Sparse Residency: Performed by all `OpImageSparse*` instructions.

* 
(s,t,r,q,a) to (u,v,w,a) Transformation, Wrapping, and Weight Image
Sampling: Performed by `OpImageWeightedSample*` instructions.

* 
(s,t,r,q,a) to (u,v,w,a) Transformation, Wrapping, and Block Matching:
Performed by `opImageBlockMatch*` instructions.

* 
(s,t,r,q,a) to (u,v,w,a) Transformation, Wrapping, and Box Filter
Sampling: Performed by `OpImageBoxFilter*` instructions.

`OpImageQuerySize`, `OpImageQuerySizeLod`, `OpImageQueryLevels`,
and `OpImageQuerySamples` query properties of the image descriptor that
would be accessed by a shader image operation.
They return 0 if the bound descriptor is a null descriptor.

`OpImageQuerySizeLod` returns the size of the image level identified by
the `Level` `of` `Detail` operand.
If that level does not exist in the image,
and the descriptor is not null,
then the value returned is **undefined**.

`OpImageQueryLod` returns the LOD parameters that would be used in an
image operation with the given image and coordinates.
If the descriptor that would be accessed is a null descriptor then
(0,0) is returned.
Otherwise, the
steps described in this chapter are performed as if for
`OpImageSampleImplicitLod`, up to [Scale Factor Operation, LOD Operation and Image Level(s) Selection](#textures-lod-and-scale-factor).
The return value is the vector (λ', dl - levelbase).
These values **may** be subject to implementation-specific maxima and minima
for very large, out-of-range values.
