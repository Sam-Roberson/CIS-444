# CIS-444 Lecture-12 Pt.2

# Create a Table View

In this lesson, you create a second, table view-based scene, that lists the cook programs . This cook program list becomes the initial scene for your app. You also design custom table cells to display each cook program.


## Learning Objectives

At the end of the lesson, you’ll be able to:

* [x] Create a second storyboard scene
* [x] Understand the key components of a table view
* [x] Create and design a custom table view cell
* [x] Understand the roles of table view delegates and data sources
* [x] Use an array to store and work with data
* [x] Display dynamic data in a table view

## Create the Cook Program List

So far, the guided cook program app has a single [scene](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW62), that is, a single screen of content. In a storyboard, each scene contains views managed by that a view controller, and any items added to the controller or its views (for example, Auto Layout constraints). A view is a rectangular region that can draw its own content and respond to user events. Views are instances of the `UIView` `class or one of its subclasses. In the CaptionThat app, we had a  scene containing the view controller’s content view, and all of the subviews you added in Interface Builder (the stack view, label, text field, image view).


Now it’s time to create another scene that shows the entire list of cook programs. Fortunately, iOS comes with a built-in class, `UITableView`, designed specifically to display a scrolling list of items. A table view is managed by a table view controller (`UITableViewController`). `UITableViewController` is a [subclass](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW14) of `UIViewController`, which is designed to handle table view-related logic. You’ll create the new scene using a table view controller. The controller displays and manages a table view. In fact, the table view is the controller’s content view, and fills the entire space available to the scene.

### To add a scene with a table view to your storyboard

1. Open your [storyboard](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW8), `Main.storyboard`.
2. Open the [Object library](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW54) in the utility area. (Alternatively, choose View > Utilities > Show Object Library.)
3. In the Object library, find a Table View Controller object.
4. Drag a Table View Controller object from the list, and drop it on the [canvas](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW6) to the left of the existing scene.

If you try to drag the table view to the canvas and nothing happens, you’re probably dragging a table view object rather than a table view controller object. The table view object is just a view representing the table itself. Like other view objects, it must be added as a subview to an existing scene. On the other hand, the table view controller is a full scene. It includes both a table view and the controller that manages the table view.

![inline][table-view-controller-obj-img]


You now have two scenes, one for displaying the cook programs list and that does nothing

![inline][added-table-view-controller-img]

It makes sense to have the cook program list be the first thing users see when they launch your app, so tell Xcode that’s your intent by setting the cook program list as the first scene.

✅ point: Set your new cook program list as the initial scene in the storyboard. If you don't remember how to do that, google it or refer back to your coding assignment guide

 🛑Do not advance until your table view controller is the initial view controller. If done correctly, it should look something like this:

![inline][initial-scene-table-img]

The table view controller is set as the initial view controller in your storyboard, making the cook program list the first scene that loads on app launch.

✅ point: Run your app. Instead of the seeing a blank screen, you should now see an empty table view—a screen with a number of horizontal dividers to separate it into rows, but with no content in each row.

![inline][empty-table-controller-img]


You need to change a few settings on this table view so you can use it in your app.

### To configure the table view

1. In your storyboard, open the [outline view](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW56) and expand the [utility area](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW72).

2. In the outline view, select Table View.
    The table view is nested under Table View Controller Scene > Table View Controller. You may have to click the disclosure triangles next to those objects to see the nested table view.

![inline][table-view-in-navigator-img]

3. With the table view selected, open the Size inspector in the utility area.
Size Inspector: 

![inline](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Art/inspector_size_2x.png)

4. In the Size inspector, find the field labeled Row Height and type `90`. Press Return.

You’ll come back to working on the table view itself in a little while, after you design an interface for what the table view displays: its table view cells.


## Design Custom Table Cells

The individual rows in a table view are managed by table view cells (`UITableViewCell`), which are responsible for drawing their contents. Table view cells come with a variety of predefined behavior and default cell styles; however, because you have more content to display in each cell than the default styles allow, you’ll need to define a custom cell style.

### To create a subclass of UITableViewCell

1. Expand the Navigator area and open the Project navigator.
2. Choose File > New > File (or press Command-N).
3. At the top of the dialog that appears, select iOS.
4. Select Cocoa Touch Class, and click Next.
5. In the Class field, type `CookProgram`
6. In the “Subclass of” field, select  `UITableViewCell`.
The class title changes to `CookProgramTableViewCell`.  Xcode makes it clear from the naming that you’re creating a custom table view cell, so leave the new name as is.
7. Make sure the Language option is set to Swift.
8. Click Next.
The save location defaults to your project directory.
The Group option defaults to your app name, YourAppName.
9. In the Targets section, make sure your app is selected and the tests for your app are unselected.
10. Click Create.
Xcode creates a file that defines the `CookProgramTableViewCell` class: `CookProgramTableViewCell.swift`
11. In the Project navigator, reposition the   `CookProgramTableViewCell.swift` file under the other Swift files, if necessary.

✅point: Your `CookProgramTableViewCell.swift` should look like this

```swift
import UIKit

class CookProgramTableViewCell: UITableViewCell {

    override func awakeFromNib() {
        super.awakeFromNib()
        // Initialization code
    }

    override func setSelected(_ selected: Bool, animated: Bool) {
        super.setSelected(selected, animated: animated)

        // Configure the view for the selected state
    }

}
```

Now, open your storyboard again.

If you look at the cook program list scene in your storyboard, you’ll notice that it shows a single table view cell.

![inline][empty-table-view-storyboard-img]

This cell is a prototype cell for the table. You can define the design and behavior of this cell. The table can then create instances of this cell. But first, you need to connect the table view cell in your scene to the custom cell subclass you just created.

### To configure a custom cell for your table view

1. In the outline view, select Table View Cell.

The cell is nested under Table View Controller Scene > Table View Controller > Table View. You may have to disclose those objects to see the table view cell.

![inline][table-view-cell-storyboard-img]


2. With the table view cell selected, open the Attributes inspector in the utility area.

3. In the Attributes inspector, find the field labeled Identifier and type `CookProgramTableViewCell`. Press Return.

![inline][cell-identifier-img]

You will use this identifier to create instances of this prototype cell.


4. Open the Size inspector

5. In the Size inspector, find the field labeled Row Height and type `90`. Make sure the `Automatic` checkbox next to this field is selected.

6. Open the Identity inspector

![inline][identity-inspector-img]

7. In the Identity inspector, find the Class field and select `CookProgramTableViewCell`.

![inline][cook-program-as-cell-img]

With the cell configured, you can design its custom user interface directly in the storyboard. You’ll need two labels and an image view. 

### Add a default photo

First, drag the below default image  below into your xcode project. Add it to your asset library and name it `defaultPhoto`.
🛑 If you don't remember how to add an image to your asset library, google it. 
![inline](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Art/defaultphoto_2x.png)


### To design the interface of the custom table cell
1. Use the Object library to find an Image View object and drag it onto the table cell.

2. Drag and resize the image view so that it’s square, flush against the left, top, and bottom of the cell.

![inline](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Art/CTV_imageview_resize_2x.png)

3. With the image view selected, open the Attributes inspector in the Utility area.


4. Once you have a In the Attributes inspector, find the Image field and select `defaultPhoto`. 

![inline](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Art/CTV_imageview_setdefault_2x.png)


5. Use the Object library to find a Label object and drag it onto the table cell. You will use the label to show the cook program's name.

6. Drag the label so that its lined up with the guidelines to the right side of the image view and to the top margin of the table view cell.

![inline](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Art/CTV_label_drag_2x.png)

7. Resize the label so that its right edge stretches to the cell’s right margin.

![inline](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Art/CTV_label_resize_2x.png)


✅point: Run your app. The table view cells now look taller. But even though you added all the necessary user interface elements to your table view cells, they’re showing up empty, just like before. Why’s that?

![inline](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Art/CTV_sim_wideemptycells_2x.png)

In a storyboard, you can configure a table view to display static data (supplied in the storyboard) or dynamic data (programmatically supplied by the table view controller). By default, the table view controller uses dynamic data. This means the interface you created in the storyboard is simply a prototype for your cell. You still need to create instances of this cell in code and fill them with your app’s data.


✅point: *Preview your interface*  (if you don't rememebr how to do that, refer to the guide in Wednesday's lecture)
Note: If you see the wrong scene in the preview, make sure to select the table view scene by clicking its scene [dock](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW63).

![inline][preview-table-view-img]


### Add Images to Your Project

Next, you need to add a few sample images to your project. You’ll use these images when you load initial cook program data into your app.

You can find sample images within the Images/ folder of the downloadable file at the end of this lesson, or use your own images. (Just make sure the names of the images you use match the image names in the code later.)

###  To add images to your project

1. If the assistant editor is open, return to the standard editor by clicking the Standard button.

Open the project navigator and utility area by clicking the Navigator and Utilities buttons in the Xcode toolbar.

2. In the project navigator, select `Assets.xcassets` to view the asset catalog.
Recall that the asset catalog is a place to store and organize your image assets for an app.

3. ~Double-click the folder name and rename it `Sample Images`.~

4. With the folder selected, in the bottom left corner, click the plus (+) button and choose New Image Set from the pop-up menu.

5. Double-click the image set name and rename it to a name you’ll remember when you’re writing it in code.

6. On your computer, select the image you want to add.

7. Drag and drop the image into the 2x slot in the image set.

8. Repeat steps 5–8 for as many images as you like. In this lesson it is assumed that you have three different images named cookProgram1, cookProgram2, and cookProgram3.

### Connect the Table Cell UI to Code

Before you can display dynamic data in your table view cells, you need to create [outlet](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW55) connections between the prototype in your storyboard and the code that represents the table view cell in `CookProgramTableViewCell.swift`.



### To connect the views to the `CookProgramTableViewCell.swift `code

1. In your storyboard, select the label in the table view cell.
2.  Click the Assistant button in the Xcode toolbar to open the assistant editor.
3. In the editor selector bar, which appears at the top of the assistant editor, switch the assistant editor from Preview to Automatic > `CookProgramTableViewCell.swift`.
4. In `CookProgramTableViewCell.swift`, find the class line, which should look like this:

```swift
class CookProgramTableViewCell: UITableViewCell {
```
5. Below the class line, add the following:

```swift
//MARK: Properties
```
6. Control-drag from the label on your canvas to the code display in the editor on the right, stopping the drag at the line below the comment you just added in `CookProgramTableViewCell.swift`.


7. In the dialog that appears, for Name, type `nameLabel`. Leave the rest of the options as they are.

8. Click Connect.

9. In your storyboard, select the image view in the table view cell.

10. Control-drag from the image view on your canvas to the code display in the editor on the right, stopping the drag at the line just below the `nameLabel` property in `CookProgramTableViewCell.swift`.

11. In the dialog that appears, for `Name`, type `photoImageView`.
Leave the rest of the options as they are, and click Connect.

12. In your storyboard, select the description Label in the tableview cell 

13. Control-drag from the description label on your canvas to the code display in the editor on the right, stopping the drag at the line just below the photoImageView property in `CookProgramTableViewCell.swift`.

14. Leave the rest of the options as they are, and click Connect.

Your outlets should look like this

```swift
@IBOutlet weak var nameLabel: UILabel!
@IBOutlet weak var descriptionLabel: UILabel!
@IBOutlet weak var photoImageView: UIImageView!
```

## Load Initial Data

To display any real data in your table cells, you need to write code to load that data. At this point, you have a data model for a cook program: the `CookProgram` class. You also need to keep a list of those cook programs. The natural place to track this is in a custom view controller subclass that’s connected to the cook program list scene. This view controller will manage the view that displays the list of Cook Programs, and have a reference to the data model behind what’s shown in the user interface.

### First, create a custom table view controller subclass to manage the cook program list scene.


### To create a subclass of UITableViewController

1. Choose File > New > File (or press Command-N).
2. At the top of the dialog that appears, select iOS, and then select Cocoa Touch Class.
3. Click Next.
4. In the Class field, type `CookProgram`
5. In the “Subclass of” field, select UITableViewController.
The class title changes to `CookProgramTableViewController`. Leave that as is.
6. Make sure the “Also create XIB file” option is unselected.
XIB files are an older way of designing the views managed by a view controller. They predate storyboards and basically represent a single scene from a storyboard. You won’t need an XIB file for this view controller, because you have already defined its content in the app’s storyboard.
7. Make sure the Language option is set to Swift.
8. Click Next.
The save location defaults to your project directory.
The Group option defaults to your app name, `YourProgramName`
In the Targets section, your app is selected and the tests for your app are unselected.
9. Leave these defaults as they are, and click Create.

Xcode creates `CookProgramTableViewController.swift` a source code file that defines your custom table view controller subclass.

10. If necessary, in the Project navigator, drag the `CookProgramTableViewController.swift` file so that it’s positioned with the other Swift files.

In this custom subclass, you can now define a property to store a list of CookProgram objects. The Swift standard library includes a structure called Array that works well for tracking lists of items.


#### To load the initial data

1. If the assistant editor is open, return to the standard editor by clicking the Standard button.
Expand the project navigator and utility area by clicking the Navigator and Utilities buttons in the Xcode toolbar.

2. Open `CookProgramTableViewController.swift`

3. Below the class line in `CookProgramTableViewController.swift`, add the following code:

```swift
//MARK: Properties
 
var cookPrograms = [CookProgram]()

```

This code declares a property on `CookProgramTableViewController` and initializes it with a default value (an empty array of `CookProgram` objects). By making cookPrograms a variable (var) instead of a constant, you make the array mutable, which means you can add items to it after you initialize it.

4. The table view controller template includes a number of method stubs and commented out methods. These are placeholder implementations that you can uncomment and expand to define the table’s appearance and behavior. You will look at these methods after you have the model data set up. For now, scroll past all the template methods, and add the following code before the final closing brace (}):

```
//MARK: Private Methods
 
private func loadSampleCookPrograms() {
    
}
```
This is a helper method to load sample data into the app.

5. In the `loadSampleCookPrograms()` method, start by loading the three cook program images:

```swift
let photo1 = UIImage(named: "asparagus")
let photo2 = UIImage(named: "bagel")
let photo3 = UIImage(named: "brownies")
let photo4 = UIImage(named: "carrots")

```
Make sure the names of the images in your project match the names you write in this code.

6. After loading the images, create three cook program objects.

```swift
        guard let cookProgram1 = CookProgram(name: "Roasted Asparagus", photo: photo1, description: "Salty and savory, the roasting method kills the natural bitterness of asparagus. Try it next to grilled fish or lamb.") else {
            fatalError("Unable to instantiate cookProgram1")
        }
         
        guard let cookProgram2 = CookProgram(name: "Toasted Bagel", photo: photo2, description: "Creates a crust that's dense and chewy, but tender and easy to bite through.") else {
            fatalError("Unable to instantiate cookProgram2")
        }
         
        guard let cookProgram3 = CookProgram(name: "Chocolate Brownies", photo: photo3, description: "Perfect crisp crackly top, super fudgy centre, chewy or gooey in all the right places, studded with melted chunks of chocolate.") else {
            fatalError("Unable to instantiate cookProgram3")
        }
        
        guard let cookProgram4 = CookProgram(name: "Roasted Carrots", photo: photo4, description: "Buttery, tender carrots roasted with the best sauce!") else {
                fatalError("Unable to instantiate cookProgram3")

            }

```
Because the `CookProgram`'s class’s initializer is failable, you need to check the result returned by the initializer. In this case, you are passing valid parameters, so the initializer should never fail. If the initializer does fail, you have a bug in your code. To help you identify and fix any bugs, if the initializer does fail, the fatalError() function prints the error message to the console and the app terminates.

7. After creating the `CookProgram` objects, add them to the `cookPrograms` array using this code:

```swift
cookPrograms += [cookProgram1, cookProgram2, cookProgram3, cookProgram4]
``` 

🛑  `cookPrograms += [cookProgram1, cookProgram2, cookProgram3, cookProgram4]` is one approach to adding objects to an array. There are many other ways to accomplish this.
✏️ Implement *a different* way to add `cookProgram1`, `cookProgram1`, `cookProgram2`, `cookProgram3`, `cookProgram4` to the `cookPrograms` array. [Apple Array Docs](https://developer.apple.com/documentation/swift/array)


8. Find the `viewDidLoad()` method. The template implementation looks like this:

```swift
override func viewDidLoad() {
    super.viewDidLoad()
    
    // Uncomment the following line to preserve selection between presentations
    // self.clearsSelectionOnViewWillAppear = false
    
    // Uncomment the following line to display an Edit button in the navigation bar for this view controller.
    // self.navigationItem.rightBarButtonItem = self.editButtonItem()
}
```
The template implementation of this method includes comments that were inserted by Xcode when it created `CookProgramTableViewController.swift`. Code comments like this provide helpful hints and contextual information in source code files, but you don’t need them for this lesson.

9. In the `viewDidLoad()` method, delete the comments and add this code after the call to `super.viewDidLoad()` to load the sample cook program data:


```swift
// Load the sample data.
loadSampleCookPrograms()
```

When the view loads, this code calls the helper method you just wrote to load the sample data. You separated this into its own method to make your code more modular and readable.

Your `viewDidLoad()` method should look like this:

```swift
override func viewDidLoad() {
    super.viewDidLoad()
    
    // Load the sample data.
    loadSampleCookPrograms()
}
```

And your `loadSampleCookPrograms()` method should look something like this:

```swift
private func loadSampleCookPrograms() {
    let photo1 = UIImage(named: "asparagus")
    let photo2 = UIImage(named: "bagel")
    let photo3 = UIImage(named: "brownies")
    let photo4 = UIImage(named: "carrots")
    
    guard let cookProgram1 = CookProgram(name: "Roasted Asparagus", photo: photo1, description: nil) else {
        fatalError("Unable to instantiate cookProgram1")
    }
     
    guard let cookProgram2 = CookProgram(name: "Toasted Bagel", photo: photo2, description: nil) else {
        fatalError("Unable to instantiate cookProgram2")
    }
     
    guard let cookProgram3 = CookProgram(name: "Chocolate Brownies", photo: photo3, description: nil) else {
        fatalError("Unable to instantiate cookProgram3")
    }
    
    guard let cookProgram4 = CookProgram(name: "Roasted Carrots", photo: photo4, description: nil) else {
            fatalError("Unable to instantiate cookProgram3")

        }
    cookPrograms += [cookProgram1, cookProgram2, cookProgram3, cookProgram4]

}
```


✅point: Build your project by choosing Product > Build. It should build without errors. Note: At this point, you may see an Xcode warning related to the fact that there’s no way to reach the View Controller scene in the app. You will fix that in the next lesson. For the rest of this lesson, just ignore it.


### Display the Data



At this point, your custom table view controller subclass, `CookProgramTableViewController`, has a mutable array that’s prepopulated with some sample cook programs. Now you need to display this data in the user interface.

To display dynamic data, a table view needs two important helpers: a data source and a delegate. A table view data source, as implied by its name, supplies the table view with the data it needs to display. A table view delegate helps the table view manage cell selection, row heights, and other aspects related to displaying the data. By default, `UITableViewController` and its subclasses adopt the necessary protocols to make the table view controller both a data source (UITableViewDataSource protocol) and a delegate (`UITableViewDelegate` protocol) for its associated table view. Your job is to implement the appropriate protocol methods in your table view controller subclass so that your table view has the correct behavior.

A functioning table view requires three table view data source methods.

```swift
func numberOfSections(in tableView: UITableView) -> Int
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell
```

The first of these is `numberOfSections(In:)`, which tells the table view how many sections to display. Sections are visual groupings of cells within table views, which is especially useful in table views with a lot of data. For a simple table view like the one in the Cooking Plus app, you just need the table view to display a single section, so the implementation of the `numberOfSections(In:)` data source method is straightforward.

### To display a section in your table view

1. In `CookProgramTableViewController.swift`, find the `numberOfSections(In:)` data source method. The template implementation looks like this:

```swift
override func numberOfSections(in tableView: UITableView) -> Int {
    // #warning Incomplete implementation, return the number of sections
    return 0
}
```

2. Change the return value from 0 to 1, and remove the warning comment.

```swift
override func numberOfSections(in tableView: UITableView) -> Int {
    return 1
}
```

This code makes the table view show 1 section instead of 0. You removed the comment that says `#warning Incomplete implementation` because you’ve completed the implementation.

The next data source method, `tableView(_:numberOfRowsInSection:)`, tells the table view how many rows to display in a given section. Your table view has only a single section, and each CookProgram object should have its own row. That means that the number of rows should be the number of CookProgram objects in your cookPrograms array.

### To return the number of rows in your table view

1. In `CookProgramTableViewController.swift`, find the `tableView(_:numberOfRowsInSection:)` data source method. The template implementation looks like this: 

```swift
override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    // #warning Incomplete implementation, return the number of rows
    return 0
}
```

You want to return the number of cook programs you have. Array has a property called `count` that returns the number of items in the array, so the number of rows is cookPrograms.count.

2. Change the `tableView(_:numberOfRowsInSection:)` data source method to return the appropriate number of rows, and remove the warning comment.

```swift
override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return cookPrograms.count
}
```

The last data source method, `tableView(_:cellForRowAt:)`, configures and provides a cell to display for a given row. Each row in a table view has one cell, and that cell determines the content that appears in that row and how that content is laid out.

For table views with a small number of rows, all rows may be onscreen at once, so this method gets called for each row in your table. But table views with a large number of rows display only a small fraction of their total items at a given time. It’s most efficient for table views to ask for only the cells for rows that are being displayed, and that’s what `tableView(_:cellForRowAt:)` allows the table view to do.

For any given row in the table view, you configure the cell by fetching the corresponding CookProgram in the cookPrograms array, and then setting the cell’s properties to corresponding values from the `CookProgram` class.

### To configure and display cells in your table view

1. In `CookProgramTableViewController.swift`, find and uncomment the `tableView(_:cellForRowAt:)` data source method. (To uncomment the method, remove the /* and */ characters surrounding it.)

After you do that, the template implementation looks like this:

```swift
override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: "reuseIdentifier", for: indexPath)
    
    // Configure the cell...
    
    return cell
}
```

The `dequeueReusableCell(withIdentifier:for:)` method requests a cell from the table view. Instead of creating new cells and deleting old cells as the user scrolls, the table tries to reuse the cells when possible. If no cells are available, `dequeueReusableCell(withIdentifier:for:)` instantiates a new one; however, as cells scroll off the scene, they are reused. The identifier tells dequeueReusableCell(withIdentifier:for:) which type of cell it should create or reuse.

To make this code work for your app, you’ll need to change the identifier to the prototype cell identifier you set in the storyboard (`CookProgramTableViewCell`), and then add code to configure the cell.

👉 Reminder: 👈
![inline][cell-identifier-img]


2. Add code at the beginning of the method, before the rest of the template implementation:

```swift
// Table view cells are reused and should be dequeued using a cell identifier.
let cellIdentifier = "CookProgramTableViewCell"
```
This creates a constant with the identifier you set in the storyboard.

3. Update the template’s identifier to the `cellIdentifier` variable. The second line of code in the method should now look like this:

```swift
let cell = tableView.dequeueReusableCell(withIdentifier: cellIdentifier, for: indexPath)
```

4. Because you created a custom cell class that you want to use, [downcast](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/GlossaryDefinitions.html#//apple_ref/doc/uid/TP40015214-CH12-SW87) the type of the cell to your custom cell subclass, `CookProgramTableViewCell`.

```swift
guard let cell = tableView.dequeueReusableCell(withIdentifier: cellIdentifier, for: indexPath) as? CookProgramTableViewCell  else {
    fatalError("The dequeued cell is not an instance of CookProgramTableViewCell.")
}
```

There’s a lot going on in this code:

* The `as? CookProgramTableViewCell` expression attempts to downcast the returned object from the UITableViewCell class to your `CookProgramTableViewCell` class. This returns an optional.
* The guard let expression safely unwraps the optional.
* If your storyboard is set up correctly, and the `cellIdentifier` matches the identifier from your storyboard, then the downcast should never fail. If the downcast does fail, the `fatalError()` function prints an error message to the console and terminates the app.

5. After the`guard` statement, add the following code:

```swift
// Fetches the appropriate cook program for the data source layout.
let cookProgram = cookPrograms[indexPath.row]
```

This code fetches the appropriate cook program from the `cookPrograms` array.

6. Now, use the cookProgram object to configure your cell. Replace the `// Configure the cell` comment with the following code:

```swift
cell.nameLabel.text = cookProgram.name
cell.descriptionLabel.text = cookProgram.description
cell.photoImageView.image = cookProgram.photo
```

This code sets each of the views in the table view cell to display the corresponding data from `cookProgram` object.

Your `tableView(_:cellForRowAt:)` method should look like this:

```swift
 override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cellIdentifier = "CookProgramTableViewCell"
        guard let cell = tableView.dequeueReusableCell(withIdentifier: cellIdentifier, for: indexPath) as? CookProgramTableViewCell  else {
            fatalError("The dequeued cell is not an instance of CookProgramTableViewCell.")
        }

        // Fetches the appropriate cook program for the data source layout.
        let cookProgram = cookPrograms[indexPath.row]
        
        cell.nameLabel.text = cookProgram.name
        cell.descriptionLabel.text = cookProgram.description
        cell.photoImageView.image = cookProgram.photo

        return cell
    }
```

The final step to displaying data in the user interface is to connect the code defined in `CookProgramTableViewCell.swift` to the cook program list scene.

### To point the Table View Controller to `CookProgramTableViewCell.swift`

1. Open your storyboard.
2. Select the table view controller by clicking on its scene dock until the entire scene has a blue outline around it.

![inline][set-cell-class-img]

3. Open the Identity inspector image: ![inline](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Art/inspector_identity_2x.png)

4. In the Identity inspector, find the field labeled Class, and select `CookProgramTableViewController`.

![inline][inspector-cook-program-table-view-controller]

✅point: Run your app. The list of items you added in the `viewDidLoad()` method should show up as cells in your table view. 

![inline][cook-programs-table-view]

## Sorting your Data

### Discussion

Currently, we display the list of cook programs based on the order in which we added them to our `cookPrograms` array: 
In other words, 
The `CookProgram` item at `cookPrograms`' index `0` is displayed first, 
The `CookProgram` item at index `1` is displayed next, etc etc

Eventually, our list of cook programs is going to grow, making it difficult for  a user to find a specific cook program. Let's help them out and display the cook programs alphabetically by a `CookProgram`'s name.

### Sorting your data

`CookProgram` is a custom object sorting it is a little different from sorting a list of strings.

1. Review the Swift Documentation or google *how to sort an array of custom objects* (in this case `CookProgam`). Implement a way to sort and display our cook programs alphabetically.

(There are several ways to do this.)

2. Add your logic to sort `cookPrograms` to the last line in your `loadSampleCookPrograms()` 

```swift
    var unorderedCookPrograms = <original cook program array>
      <add your sorted logic here>
      /// assign your sorted cook programs array to your cook programs
    self.cookPrograms =  <your sorted array of cook programs>
```

🛑❗️🛑❗️🛑❗️🛑❗️ Once you have a solution, raise your hand and I will give you the OK to proceed. Make sure you understand and can explain your solution.🛑❗️🛑❗️🛑❗️🛑❗️🛑❗️

3. Run your app. The list should display alphabetically. 

![inline][sorted-cook-programs-table-view-img]



[added-table-view-controller-img]:resources/added-table-view-controller.png

[table-view-controller-obj-img]:resources/table-view-controller-obj.png

[initial-scene-table-img]:resources/initial-scene-table.png

[empty-table-controller-img]:https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Art/CTV_sim_emptytv_2x.png

[table-view-in-navigator-img]:resources/table-view-in-navigator.png

[empty-table-view-storyboard-img]: https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Art/CTV_singletvcell_2x.png

[table-view-cell-storyboard-img]:resources/table-view-cell-storyboard.png

[cook-program-as-cell-img]:resources/cook-program-as-cell.png

[identity-inspector-img]:https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Art/inspector_identity_2x.png

[preview-table-view-img]:resources/preview-table-view.png

[cell-identifier-img]:resources/cell-identifier.png

[set-cell-class-img]:resources/set-cell-class.png

[inspector-cook-program-table-view-controller]:resources/Identity-Inspector-CookProgramTVC.png

[cook-programs-table-view]:resources/cook-programs-table-view.png

[sorted-cook-programs-table-view-img]:resources/sorted-cook-programs-table-view.png
