# xblock-hl_text
pip package for custom xblock to present users with custom build of CKEditor 5.

This xblock was designed to be inheritable by other xblocks to
provide a custom ckeditor 5 editor provided an overridable empty template to be
displayed if no content is stored.

To specify a default empty (or starter) template in an inheriting xblock, override the
`get_empty_template` method and return a `render_template` call specifying the
path the local template. an example of a basic xblock inheriting from HL_Text is provided below:

*NOTE: any pip packages that inherit from this package must list `xblock-hl-text` as a required install package*

```
# import the hydrolearn custom text xblock
from hl_text import HLCustomTextXBlock

# inherit from the custom text xblock
class HL_Text_Child(HLCustomTextXBlock):

    # provide an override for the new child's display name so it doesn't appear
    #   as 'HydroLearn Text Block' in the cms view.
    display_name = String(
        display_name="HL text child xblock",
        help="This name appears in the horizontal navigation at the top of the page",
        scope=Scope.settings,
        default="HL Text Child"
    )

    # override the 'get_empty_template' method providing the path to the starter template
    def get_empty_template(self, context={}):
        return render_template('templates/initial_learning_activity_template.html', context)


```




## Building the Package

### Requirements
- python installed
- pip installed
- pip wheel installed

#### Additional helpful packages
- if modifying styles, you will need a sass compiler, if using windows I recommend Koala (http://koala-app.com/).
  - unfortunately I do not have a recommendation for Linux based sass compilers, but if I recall correctly there are several python packages which can accomplish the task.

### Build Process
- Download the project
- navigate to the project's root directory in a terminal session
- run `python setup.py bdist_wheel`
 - this will generate the following in the root directory
   - a `build` directory (excluded from repository by default)
   - a `dist` directory (excluded from repository by default)
   - additionally this will update the contents of the `xblock_hl_text.egg-info` directory to update the list of sources for the package
