# DG-Content - DIAGRAMMAR in HTML
Author: Mark Hakkinen - Educational Testing Service
## About
`DG-Content` is an initial prototype of a custom elements/webcomponents implementation of the DIAGRAMMAR markup for image description directly in HTML.  This allows image description and alternate formats of the image to be authored and directly accessible in HTML. Using a model similar to that of HTML media elements (i.e., `AUDIO` and `VIDEO`), `DG-Content` can provide a default user interface for exposing the presence of image description and alternates to end users, or the developer may elect to implement their own user interface via javascript.

## Requirements
This implementation uses [polymer](http://www.polymer-project.org).  No other libraries are used.

## DG-Content explained
`DG-Content` is an initial prototype, and as such is neither complete nor should it be considered a definitive model for mapping DIAGRAMMAR to HTML. DG-Content differs also from DIAGRAMMAR in that the image itself is contained within the DG-Content container.

The following sections describe the DG-Content Structure. Attributes or elements not presently implemented are noted.
### Example of DG-Content Usage
```
<dg-content controls>
   <dg-img>
   <img src="imgs/survey.jpg" alt="Image of surveyors working">
  </dg-img>
  <dg-summary show>
    The image depicts two surveyors measuring the angles between
    themselves and a tree.
  </dg-summary>
  <dg-longdesc show="true" overlay="false">Two surveyors, A and P, stand some distance 
    apart on the south bank 
	of a river, looking at a tree, T, that is on the north bank of the river. 
	Points A, P, and T form a triangle. At points A and P, there are two parallel 
	sight lines pointing north and forming angles outside of the triangle. At 
	point P, angle TPA is 53 degrees. The adjacent angle between PT and the 
	northern sight line is 37 degrees. At point A, angle TAP is not labeled, 
	and the adjacent angle formed between AT and that northern sight line is 
	32 degrees.
  </dg-longdesc>
  <dg-simplifieddesc show="false">
    T, A, and P are the three points on a triangle. Angle TPA is 53 degrees 
	with an adjacent angle of 37 degrees. The angle adjacent to angle TAP is 32 degrees.
  </dg-simplifieddesc>
  <dg-tactile show="false" source="imgs/anglesmap.jpg" controls="false">
    <dg-tour>
      Start exploring at the top right.
    </dg-tour>
  </dg-tactile>
</dg-content>
```
### Elements & Attributes
#### `<dg-content>`
Top level container element.
#####Attributes
`controls` true | false  (optional)
Indicates that default user interface will be supplied for all applicable alternative content. `Controls` without explict value is true.
`src` URI (optional) NOT IMPLEMENTED
As an alternate to supplying the DIAGRAMMAR content inline in HTML, the author may reference an external DIAGRAMMAR resource file via URI. The alternate content will be dynamically loaded into the appropriate structures within DG-Content in the containing page.
#### `<dg-img>`
A container for the image resource.  The image may be any of the formats supported by the browser, and may utilize, for example, an `img` element, `svg`, or ASCII art. 
##### Attributes
*none at this time*
#### `<dg-summary>`
Container for the image summary. Can contain structured text.
##### Attributes
`show` true | false  (optional)
Indicates whether the summary will be automatically shown along with the image. `show` without explict value is true.
*Note* - placement of the summary text is up to discussion, and whether styling options are provided.
#### `<dg-longdesc>`
The container for the image's long description, which can be rich structured text.  TBD is whether `dg-longdesc` would allow for a `src` attribute pointing to an external text description.
##### Attributes
`show` true | false  (optional)
Indicates whether the long description will be automatically shown along with the image. `show` without explict value is true.
`overlay` true | false (optional)
Indicates how the long description will be shown. If `overlay` is true, the description will be shown as an overlay upon the image.  If false, the description will be placed below the image.
*Note* - this feature was added as an experiment to demonstrate how styles may be applied to the alternates. A richer styling mechanism would be needed.
#### `<dg-simplifieddesc>`
The container for the image's simplified description, which can be rich, structured text.
##### Attributes
`show` true | false  (optional)
Indicates whether the simplified description will be automatically shown along with the image. `show` without explict value is true.
#### `<dg-tactile>`
Element referencing a tactile file for printing or embossing.
*Note* This element needs further discussion.
#####Attributes
`show` true | false  (optional)
Indicates whether the Emboss button will be automatically shown along with the image. `show` without explict value is true.
`src` URI 
Reference to the tactile image file.
`type` embossable | 3D | other    NOT IMPLEMENTED
The type of tactile file
#### `<dg-tour>`
Child element of `<dg-tactile>` containing a rich, structured text tour of the tactile image or object.
*Note* Discussion needed as to when and how this text would be displayed.
### Javascript Interface
`<dg-content>` can be controlled via Javascript, to show and hide descriptions, for example.  In the code sample below, a function `toggleLongdesc` is used to change the *show* state of `dg-longdesc`.

```
function toggleLongdesc() {
var el=document.querySelector("dg-longdesc");
if (el.getAttribute("show")) {
    el.removeAttribute("show");}
    else
    {el.setAttribute("show",true);}
    } 

```

## Acknowlegments
The image sample used is from the [DIAGRAM Center's](http://www.diagramcenter.org) [Accessible Image Sample Book](http://diagramcenter.org/standards-and-practices/accessible-image-sample-book.html).
