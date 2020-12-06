# Chapter 29 Protocols

-   UITableView object does not contain the data that it displays
    -   it has to get data from a helper object
    -   The developer who created the **UITableView** class specified the role of **UITableView**’s data source by creating the UITableViewDataSource protocol

-   A protocol can specify a role that an object can fill
-   A protocol is a list of method declaration



```objc
// Just like classes, protocols can inherit from other protocols 
// This protocol inherits from the NSObject protocol
@protocol UITableViewDataSource <NSObject>
    
 // The following methods must be implemented by any table view data source
@required
    
// A table view has sections, each section can have several rows
- (NSInteger)tableView:(UITableView *)tv numberOfRowsInSection:(NSInteger)section;

// This index path is two integers (a section and a row)
// The table view cell is what the user sees in that section/row

- (UITableViewCell *)tableView:(UITableView *)tv cellForRowAtIndexPath:(NSIndexPath *)ip;

// These methods may be implemented by a table view data source
@optional
// If data source does not implement this method, table view has only one section
- (NSInteger)numberOfSectionsInTableView:(UITableView *)tv;

// Rows can be deleted and moved
- (BOOL)tableView:(UITableView *)tv canEditRowAtIndexPath:(NSIndexPath *)ip;
- (BOOL)tableView:(UITableView *)tv canMoveRowAtIndexPath:(NSIndexPath *)ip;

- (void)tableView:(UITableView *)tv commitEditingStyle:(UITableViewCellEditingStyle)editingStyle
forRowAtIndexPath:(NSIndexPath *)ip;

- (void)tableView:(UITableView *)tv moveRowAtIndexPath:(NSIndexPath *)sourceIndexPath
toIndexPath:(NSIndexPath *)destinationIndexPath;

@end
```



-   The UITableVew class has dataSource property
    -   `@property(nonatomic, assign) id<UITableViewDataSource> dataSource;`
    -   the data source can be an object of any type, so long as the object conforms to the UITableViewDataSource protocol.
-   When you create a class to fill the role of **UITableView**’s data source, you explicitly say, “This class conforms to the UITableViewDataSource protocol” in the header file. It looks like this:

```objc
@interface TerrificViewController : UIViewController <UITableViewDataSource> ...
@end
```

