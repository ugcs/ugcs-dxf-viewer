# DXF viewer

This package provides DXF 2D viewer component written in JavaScript. It renders drawings using WebGL 
(via [three.js](https://threejs.org) library). It was carefully crafted with performance in mind, 
intended for drawing huge real-world files without performance problems.

The usage example and demo is available here: 

The package is released under the MIT License.

This is community version of the viewer. It is initially published in the
[corporate repository](https://bitbucket.org/sphengineering/dxf-viewer) and is used in production in
[Atlas](https://atlas.ugcs.com) project. There it will be mostly maintained for project-specific 
needs. The community version will receive all generic features and bug fixes.

TODO: npm

## Features

 * File fetching, parsing and preparation for rendering is separated in such a way that it can be
   easily off-loaded to web-worker using provided helpers. So the most heavy-weight processing part
   does not affect UI responsiveness. The example above demonstrates this technique.
 * Geometry batching - minimal number of rendering batches is created during file processing, thus 
   minimizing total required number of draw calls.
 * Instanced rendering - features which are rendered multiple times with different transforms (e.g.
   DXF block instances) are rendered by a single draw call using instanced rendering WebGL feature.
 * Multiple fonts support. List of fonts can be specified for text rendering. Fonts are lazy-loaded,
   once a character encountered which glyph is not yet available through already loaded fonts, next
   font is fetched and checked for the necessary glyph.
 * Layers - layers are taken into account when creating rendering batches so that they can be easily
   hidden/shown.
   
## Incomplete features

There are still many incomplete features. I will try to implement some of them when I have some 
time. Anything useful implemented in the corporate repository will be merged here as well.

 * Multiline text blocks (MTEXT group).
 * Text styling. Currently, text rendering is using just the specified fonts in the specified order.
   DXF style and font attributes are ignored. Text glyphs are always rendered infilled.
 * Line patterns - all lines are rendered in continuous style for now. I am going to use 1-D texture
   generated on preparation stage, texture coordinates (which should account pattern continuity flag
   in DXF vertices attributes), and a dedicated shader to implement this feature.
 * Line patterns with shapes (e.g. with circles).
 * Wide lines. Currently, all lines are rendered as thin lines. Physical width is not implemented.
 * Variable width lines (i.e. with start and end width specified).
 * Smoothed polyline (curve-fit/spline-fit addition vertices).
 * Hatching
 * Infilled polygons - everything is drawn with outlines now.
 * Block instancing in a grid. Grid attributes are ignored now.
 * Many less commonly used DXF features.
