#include <iostream>
#include <vector>
#include <algorithm>  // Added for find_if

using namespace std;

class Product {
public:
    int productId;
    string productName;
    double productPrice;

    Product(int id, string name, double price) : productId(id), productName(name), productPrice(price) {}
};

class Inventory {
private:
    vector<Product> products;

public:
    void addProduct(int id, string name, double price) {
        Product newProduct(id, name, price);
        products.push_back(newProduct);
        cout << "Product added to inventory.\n";
    }

    void removeProduct(int id) {
        auto it = find_if(products.begin(), products.end(), [id](const Product& p) { return p.productId == id; });

        if (it != products.end()) {
            products.erase(it);
            cout << "Product removed from inventory.\n";
        } else {
            cout << "Product not found in inventory.\n";
        }
    }

    void displayInventory() {
        cout << "Inventory:\n";
        for (const auto& product : products) {
            cout << "ID: " << product.productId << "\tName: " << product.productName << "\tPrice: $" << product.productPrice << endl;
        }
    }
};

int main() {
    Inventory myInventory;

    myInventory.addProduct(1, "Laptop", 1599.99);
    myInventory.addProduct(2, "Perfume", 179.99);
    myInventory.addProduct(3, "Headphones", 79.99);

    myInventory.displayInventory();

    myInventory.removeProduct(2);
    myInventory.removeProduct(3);

    myInventory.displayInventory();

    return 0;
}








\\ part b


#include <iostream>
#include <vector>
#include <algorithm>
#include <chrono>

using namespace std;

void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; ++i) {
        for (int j = 0; j < n - i - 1; ++j) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

int main() {
    vector<int> data(100000);

    for (int i = 0; i < 100000; ++i) {
        data[i] = 100000 - i;
    }

    auto startTime = chrono::high_resolution_clock::now();

    // Replace bubbleSort with std::sort
    sort(data.begin(), data.end());

    auto endTime = chrono::high_resolution_clock::now();

    auto duration = chrono::duration_cast<chrono::microseconds>(endTime - startTime);

    cout << "Sort Execution Time: " << duration.count() << " microseconds\n";

    cout << "First 10 elements: ";
    for (int i = 0; i < 10; ++i) {
        cout << data[i] << " ";
    }

    cout << "\nLast 10 elements: ";
    for (int i = data.size() - 10; i < data.size(); ++i) {
        cout << data[i] << " ";
    }

    // Reset data for STL sort
    for (int i = 0; i < 100000; ++i) {
        data[i] = 100000 - i;
    }

    auto startTimeSTL = chrono::high_resolution_clock::now();
    sort(data.begin(), data.end());
    auto endTimeSTL = chrono::high_resolution_clock::now();
    auto durationSTL = chrono::duration_cast<chrono::microseconds>(endTimeSTL - startTimeSTL);

    cout << "\nSTL Sort Execution Time: " << durationSTL.count() << " microseconds\n";

    cout << "First 10 elements after STL sort: ";
    for (int i = 0; i < 10; ++i) {
        cout << data[i] << " ";
    }

    cout << "\nLast 10 elements after STL sort: ";
    for (int i = data.size() - 10; i < data.size(); ++i) {
        cout << data[i] << " ";
    }

    return 0;
}
