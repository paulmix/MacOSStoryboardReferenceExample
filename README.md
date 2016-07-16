# Using Storyboard References for Embedded Views on MacOS

Setting up and using Storyboard References in Xcode for Mac OS is unintuitive, and it took me a while to figure it out.

Here are the steps necessary to properly set up and use Storyboard References so that you can define and embed view controller storyboard references so that you can reuse them in multiple places.

**IMPORTANT NOTE:** Storyboard references require a deployment target of MacOS 10.10.

1. Create a Storyboard for reusable view controller.
￼![Create Reusable Storyboard](readme_images/01-create_reusable_storyboard.png)
￼￼![Empty Reusable Storyboard](readme_images/02-empty_reusable_storyboard.png)
2. Create a view controller class for the view.
￼￼￼![Select Cocoa Class](readme_images/03-select_cocoa_class.png)
a. Make sure "Also create XiB file" is unchecked (as the interface will be defined by the storyboard you just created).
￼￼￼￼![Uncheck Use XIB](readme_images/04-uncheck_use_xib.png)
￼￼￼￼![Custom View Controller](readme_images/05-custom_view_controller.png)
3. Configure the reusable view storyboard by adding a View Controller from the Library.
￼￼￼￼![Add Reusable View Controller](readme_images/06-add_reusable_view_controller.png)
a. In the Identity Inspector, set the Custom Class of the view controller to the one you just created.
￼￼￼￼![Set Custom Class](readme_images/07-set_custom_class.png)
b. Add desired controls and define constraints in the reusable view. Note the size of the view.
￼￼￼￼![Configure Reusable View](readme_images/08-configure_reusable_view.png)
c. Specify a Storyboard ID for the reusable view controller.
￼￼￼￼￼![Specify Storyboard ID](readme_images/09-specify_storyboard_id.png)
d. Make sure "Is Initial View Controller" is checked for the reusable view controller scene.
￼￼￼￼￼￼![Set Initial View Controller](readme_images/10-set_initial_view_controller.png)
4. In the storyboard view that you wish to embed the reusable view in, add a Storyboard Reference from the library.
￼￼￼￼￼￼![Add Storyboard Reference](readme_images/11-add_storyboard_reference.png)
a. Select the Storyboard Reference in the Storyboard, then show the Attributes Inspector (this can be twitchy. When I first added the Storyboard Reference, the Inspector was blank; I had to first select the reference, then select the Quick Help Inspector, then select the other Inspectors in sequence until I got to the Attributes Inspector). Enter the reusable Storyboard ID you created above for the reference.
￼￼￼￼￼￼![Specify Storyboard Reference](readme_images/12-specify_storyboard_reference.png)
5. Still in the containing storyboard, add a Container View from the library to the view you wish to embed the reusable view in.
￼￼￼￼￼￼![Add Container View](readme_images/13-add_container_view.png)
a. Set size and constraints of the Container View appropriately.
￼￼￼￼￼￼![Configure Container View](readme_images/14-configure_container_view.png)
6. When the Container View was added, it automatically created a View Controller to be the target of the Container View's "embed" segue. We don't need this view controller, as we want the Container View to embed the Reusable View.
￼￼￼￼￼￼![Select Unneeded View Controller](readme_images/15-select_unneeded_view_controller.png)
a. Select the View Controller scene that was generated for the Container View and delete it.
￼￼￼￼￼￼￼![Delete Unneeded View Controller](readme_images/16-delete_unneeded_view_controller.png)
7. Now create a new "embed" segue from the Container View to the reusable view storyboard reference. Control drag from the Container View to the storyboard reference, and select the Embed segue.
￼￼￼￼￼￼￼![Select Embed Segue](readme_images/17-select_embed_segue.png)
![Segue To Reusable View](readme_images/18-segue_to_reusable_view.png)
8. Build and run your app. The reusable view should be embedded within the container view.
![Run App](readme_images/19-run_app.png)

￼That's it! You'll likely want to tweak constraints to make the embedded reusable view behave as you would like in the parent view.