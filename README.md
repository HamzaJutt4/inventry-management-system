# inventry-management-system
#include <iostream>
#include <iomanip> // For setw()
#include<cstring>
#include <climits>
using namespace std;
void addItem();
void updateStock();
void Remove();
void SearchItem();
void ListAllProducts();
void generate_inventory_report();
void checkStockAvailability();
void ListAllProductsSorted(int);
void sortByPrice();
void sortByQuantity();
void sortByName();
void swapItems(int i, int j);
void saleItems();
void displayGraphicalChart();


const int MAX_ITEMS = 50; // Define the maximum number of items

// Arrays to store item details
string nameofitem[MAX_ITEMS];
double priceofitem[MAX_ITEMS];
int quantity[MAX_ITEMS];
int itemid[MAX_ITEMS];
string typeofitem[MAX_ITEMS];
int salesRecord[MAX_ITEMS];

int numItems = 0;
// Function to display the menu
void displayMenu()
{


    cout <<setw(75)<< "======================================" << endl;
    cout <<setw(75)<< "      Inventory Management Menu       " << endl;
    cout <<setw(75)<< "======================================" << endl;
    cout <<setw(75)<< "=1. Add Product                      =" << endl;
    cout <<setw(75)<< "=2. Remove Product                   =" << endl;
    cout <<setw(75)<< "=3. Update Stock                     =" << endl;
    cout <<setw(75)<< "=4. Search Product                   =" << endl;
    cout <<setw(75)<< "=5. List All Products                =" << endl;
    cout <<setw(75)<< "=6. Generate Inventory Report        =" << endl;
    cout <<setw(75)<< "=7. Check Stock Availability         =" << endl;
    cout <<setw(75)<< "=8. Sort Products                    =" << endl;
    cout <<setw(75)<< "=9. Graphical representation         =" << endl;
    cout <<setw(75)<< "=10. Sell Products                   =" << endl;
    cout <<setw(75)<< "=0. Exit                             =" << endl;
    cout <<setw(75)<< "======================================" << endl;
}

int main() {
    int choice;

    do
        {
        displayMenu();
        cout << "Enter your choice (0-10): ";
        cin >> choice;

        switch (choice)
        {
            case 1:
                cout << "Adding a new product..." << endl;
                // adding a product
                addItem();
                break;
            case 2:
                cout << "Removing a product..." << endl;
                //  removing a product
                Remove();
                break;
            case 3:
                cout << "Updating stock..." << endl;
                //  updating stock
                updateStock();

                break;
            case 4:
                cout << "Searching for a product..." << endl;
                //  searching a product
                SearchItem();
                break;
            case 5:
                cout << "Listing all products..." << endl;
                //  listing all products
                ListAllProducts();
                break;
            case 6:
                cout << "Generating inventory report..." << endl;
                //  generating a report
                generate_inventory_report();
                break;
            case 7:
                cout << "Checking stock availability..." << endl;
                //  checking stock availability
                checkStockAvailability();
                break;
            case 8:
                //  sorting products
                cout << "Sorting products..." << endl;
                cout << "1. Sort by Name" << endl;
                cout << "2. Sort by Quantity" << endl;
                cout << "3. Sort by Price" << endl;
                int sortChoice;
                cout << "Enter your choice (1-3): ";
                cin >> sortChoice;
                ListAllProductsSorted(sortChoice);
                break;
                case 9:
                	//graphyical representation

                    displayGraphicalChart();

                break;
                case 10:
                		//sale records
                		saleItems();
                break;
            case 0:
                cout << "Exiting. Have a great day!" << endl;
                break;
            default:
                cout << "Invalid choice. Please try again." << endl;
        }
    } while (choice != 0);

    return 0;
}
void addItem()
{
    cout<<"Enter the number of item :";
    cin>>numItems;
    itemid[numItems]=numItems;
    
    if (numItems <= MAX_ITEMS)
        {
        cout<<"----------------------------------------"<<endl;
        cout << "Enter the name of the item: ";
        cin >> nameofitem[numItems];
        cout<<"----------------------------------------"<<endl;
        cout << "Enter the price of the item: ";
        cin >> priceofitem[numItems];
        cout<<"----------------------------------------"<<endl;
        cout << "Enter the quantity of the item: ";
        cin >> quantity[numItems];
        cout<<"----------------------------------------"<<endl;
        cout << "Enter the type of the item (frozen, dessert, regular, fragile): ";
        cin >> typeofitem[numItems];
        cout<<"----------------------------------------"<<endl;
        
        cout << "Item added successfully." << endl;
        cout<<"----------------------------------------"<<endl;
    } else {
        cout << "Inventory is full. Cannot add more items." << endl;
    }
}
// Function to update the stock of an existing item
void updateStock()
{
    string itemname;
    cout << "Enter the name of the item to update stock: ";
    cin >> itemname;

    bool found = false;
    for (int i = 1; i <= numItems; ++i) {
        if (nameofitem[i] == itemname)
            {
            found = true;
            cout<<"----------------------------------------"<<endl;
            cout<< "Enter the new price for " <<nameofitem[i] <<";";
            cin>>priceofitem[i];
            cout<<"----------------------------------------"<<endl;
            cout << "Enter the new quantity for " <<nameofitem[i] << ": ";
            cin >> quantity[i];
            cout<<"----------------------------------------"<<endl;
            cout << "Stock updated successfully." << endl;
            cout<<"----------------------------------------"<<endl;
            break;
        }
    }

    if (!found)
        {
        cout<<"----------------------------------------"<<endl;
        cout << "Item not found in inventory." << endl;
        cout<<"----------------------------------------"<<endl;
    }

}
void Remove()
{
    int itemId;
    cout << "Enter the ID of the item to remove: ";
    cin >> itemId;

    // Find the index of the item to be removed
    int indexToRemove = -1;
    for (int i = 0; i < numItems; ++i) {
        if (itemid[i+1] == itemId) {
            indexToRemove = i;
            break;
        }
    }

    if (indexToRemove != -1) {
        // Shift items to remove the selected item
        for (int i = indexToRemove; i < numItems - 1; ++i) {
            itemid[i] = itemid[i + 1];
            nameofitem[i] = nameofitem[i + 1];
            priceofitem[i] = priceofitem[i + 1];
            quantity[i] = quantity[i + 1];
            typeofitem[i] = typeofitem[i + 1];
        }
        numItems--; // Decrease the total number of items
        cout << "Item removed successfully.\n";
    } else {
        cout << "Item not found.\n";
    }
}

void SearchItem()
{
    string itemname;
    cout << "Enter the name of the item to search: ";
    cin >> itemname;
    bool found = false;
    for (int i = 1; i <= numItems; ++i)
        {
        if (nameofitem[i] == itemname)
            {
            cout<<" ---------------------------------------"<<endl;
            cout <<"|Item details:                        |"<<endl;
            cout<<" ---------------------------------------"<<endl;
            cout <<"|ID:"<< itemid[i] <<endl;
            cout<<" ---------------------------------------"<<endl;
            cout <<"|Name: " << nameofitem[i]<<endl;
            cout<<" ---------------------------------------"<<endl;
            cout <<"|Price: " << priceofitem[i]<<endl;
            cout<<" ---------------------------------------"<<endl;
            cout <<"|Quantity: " << quantity[i]<<endl;
            cout<<" ---------------------------------------"<<endl;
            found = true;
        }
    }
    if (!found)
        {
        cout<<"----------------------------------------"<<endl;
        cout << "Item not found.\n";
        cout<<"----------------------------------------"<<endl;
    }
}

void ListAllProducts()
 {
    cout << "Inventory:" << endl;
    cout << "====================================================================================" << endl;
    cout << setw(5) << "ID" << setw(20) << "Name" << setw(10) << "Price" << setw(14) << "Quantity" << setw(10) << "Type" << setw(15) << "Sales Record" << endl;
    cout << "====================================================================================" << endl;
    for (int i = 1; i <= numItems; ++i)
        {
        cout << setw(5) << itemid[i] << setw(20) << nameofitem[i] << setw(10) << priceofitem[i] << setw(10) << quantity[i] << setw(15) << typeofitem[i]<< setw(15) <<salesRecord[i];
        cout << endl;
    }
    cout << "====================================================================================" << endl;

}





void generate_inventory_report()
{
    double total_stock_value = 0;
    int highest_stock_level =0;
    int lowest_stock_level = INT_MAX;
    int highest_stock_index = 0;
    int lowest_stock_index = 0;

    // Calculate total stock value and find highest/lowest stock levels
    for (int i = 1; i <= numItems; ++i)
        {
        total_stock_value += quantity[i];
        if (quantity[i] > highest_stock_level)
            {
            highest_stock_level = quantity[i];
            highest_stock_index = i;
        }
        if (quantity[i] <=lowest_stock_level)
        {
            lowest_stock_level = quantity[i];
            lowest_stock_index = i;
        }
    }

    // Generate and print report
    cout << "Inventory Report:\n";
    cout << "==================================================================================================" << endl;
    cout << setw(20) << "Product Name" << setw(15) << "Price" << setw(15) << "Quantity" << setw(20) << "Total Value" << endl;
    cout << "==================================================================================================" << endl;

    for (int i = 1; i <= numItems; ++i)
        {
        double total_value = quantity[i] * priceofitem[i];
        cout << setw(20) << nameofitem[i] << setw(15) << priceofitem[i] << setw(15) << quantity[i] << setw(20) << total_value << endl;

    }

    cout << "===================================================================================================" << endl;
    cout << "Total Stock Value: "<<total_stock_value << endl;
    cout << "Highest Stock Level: " << nameofitem[highest_stock_index] << " - " << highest_stock_level << " units" << endl;
    cout << "Lowest Stock Level: " << nameofitem[lowest_stock_index] << " - " << lowest_stock_level << " units" << endl;
}

void checkStockAvailability()

{
        cout << "Inventory:" << endl;
    cout << "====================================================" << endl;
    cout << setw(5) << "ID" << setw(20) << "Name"<<endl;
    cout << "====================================================" << endl;
    for (int i = 1; i <= numItems; ++i)
        {
        cout << setw(5) << itemid[i] << setw(20) << nameofitem[i];
        cout << endl;
    }
    cout << "====================================================" << endl <<endl <<endl;
    int item_id;
    int requiredQuantity;

    cout << "Enter the ID of the item to check availability: ";
    cin >> item_id;

    bool check =false;
    for (int i = 1; i <= numItems; ++i)
        {
        if (itemid[i] == item_id)
        {

            cout<<"--------------------------------------------------"<<endl;
            cout << "Available Quantity of " << nameofitem[i] << ": " << quantity[i] << endl;
            cout<<"--------------------------------------------------"<<endl;
            cout << "Enter the required quantity: ";
            cin >> requiredQuantity;
            cout<<"--------------------------------------------------"<<endl;
            if (requiredQuantity > quantity[i])
                {
                cout << "Sorry, the required quantity is not available." << endl;
            }
            else if (requiredQuantity == quantity[i])
             {
                cout << "The required quantity is available. Stock will be zero after checkout." << endl;
            }
            else
             {
                cout << "The required quantity is available. Stock will be reduced after checkout." << endl;
            }
            break;
        }
    }

    check= true;
    if (!check)
        {
        cout << "Item not found in inventory." << endl;
    }


}
// Function to list all products with sorting option
void ListAllProductsSorted(int sortChoice)
{

    switch (sortChoice) {
        case 1:
            sortByName();
            cout << "Products sorted by name." << endl;
            break;
        case 2:
            sortByQuantity();
            cout << "Products sorted by quantity." << endl;
            break;
        case 3:
            sortByPrice();
            cout << "Products sorted by price." << endl;
            break;
        default:
            cout << "Invalid sort option." << endl;

    }

    // Print the sorted inventory
    cout << "Sorted Inventory:" << endl;
    cout << "====================================================================================" << endl;
    cout << setw(5) << "ID" << setw(20) << "Name" << setw(10) << "Price" << setw(14) << "Quantity" << setw(10) << "Type" << setw(20) << "Sales Record" << endl;
    cout << "====================================================================================" << endl;
    for (int i = 1; i <= numItems; ++i) {
        cout << setw(5) << itemid[i] << setw(20) << nameofitem[i] << setw(10) << priceofitem[i] << setw(10) << quantity[i] << setw(10) << typeofitem[i]<< setw(10)<<salesRecord[i];
        cout << endl;
    }
}


// Function to swap two items in the inventory arrays
void swapItems(int i, int j)
{
    swap(nameofitem[i], nameofitem[j]);
    swap(priceofitem[i], priceofitem[j]);
    swap(quantity[i], quantity[j]);
    swap(typeofitem[i], typeofitem[j]);
}

// Function to sort products by name
void sortByName()
{
    for (int i = 1; i <= numItems - 1; ++i) {
        for (int j = 1; j <= numItems - i; ++j) {
            if (nameofitem[j] > nameofitem[j + 1]) {
                swapItems(j, j + 1);
            }
        }
    }
}

// Function to sort products by quantity
void sortByQuantity()
 {
    for (int i = 1; i <= numItems - 1; ++i) {
        for (int j = 1; j <= numItems - i; ++j) {
            if (quantity[j] > quantity[j + 1]) {
                swapItems(j, j + 1);
            }
        }
    }
}

// Function to sort products by price
void sortByPrice()
{
    for (int i = 1; i <= numItems - 1; ++i)
	 {
        for (int j = 1; j <= numItems - i; ++j) {
            if (priceofitem[j] > priceofitem[j + 1]) {
                swapItems(j, j + 1);
            }
        }
    }
}
// Function to record the sale
void saleItems()
 {
    cout << "Inventory:" << endl;
    cout << "====================================================" << endl;
    cout << setw(5) << "ID" << setw(20) << "Name"<<endl;
    cout << "====================================================" << endl;
    for (int i = 1; i <= numItems; ++i)
        {
        cout << setw(5) << itemid[i] << setw(20) << nameofitem[i];
        cout << endl;
    }
    cout << "====================================================" << endl <<endl <<endl;
    int itemId, quantitySold;
    bool found = false;

    cout << "Enter the ID of the item to sell: ";
    cin >> itemId;

    for (int i = 0; i <= numItems; ++i)
	{
        if (itemid[i] == itemId)
		{
            found = true;
            cout << "Enter the quantity to sell: ";
            cin >> quantitySold;


            if (quantity[i] >= quantitySold)
			 {

                quantity[i] -= quantitySold;


                salesRecord[i] += quantitySold;

                cout << "Sale recorded successfully." << endl;
            }
			else
			 {
                cout << "Insufficient stock. Sale could not be recorded." << endl;
            }
            break;
        }
    }

    if (!found)
	{
        cout << "Item not found in inventory." << endl;
    }
}
void displayGraphicalChart()
{
    cout << "Graphical Representation:" << endl;
    cout << "---------------------------------" << endl;

    for (int i = 1; i <= numItems; ++i) {
        cout << setw(20) << left << nameofitem[i] << "|";
        for (int j = 0; j < quantity[i]; ++j) {
            cout << "*";
        }
        cout << endl;
    }
}
