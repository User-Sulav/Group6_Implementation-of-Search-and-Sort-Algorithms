# Group6_Implementation-of-Search-and-Sort-Algorithms
C++ code for Data Structures and Algorithms group assignment
#include <iostream>
#include <vector>
#include <random>
#include <algorithm> // For std::sort
using namespace std;

// Function to perform binary search on a sorted array
int binarySearch(const vector<int>& arr, int target) {
    int low = 0;
    int high = arr.size() - 1;
    
    while (low <= high) {
        int mid = low + (high - low) / 2; // Avoid overflow
        if (arr[mid] == target) {
            return mid; // Element found, return index
        } else if (arr[mid] < target) {
            low = mid + 1; // Search right half
        } else {
            high = mid - 1; // Search left half
        }
    }
    return -1; // Element not found
}

int main() {
    // Seed for random number generation
    random_device rd;
    mt19937 gen(rd());
    uniform_int_distribution<> dis(1, 1000); // Random integers between 1 and 1000

    // Input size of array
    int N;
    cout << "Enter the number of elements (N): ";
    cin >> N;
    
    // Validate input
    if (N <= 0) {
        cout << "Invalid input. N must be positive." << endl;
        return 1;
    }

    // Generate N random integers
    vector<int> arr(N);
    for (int i = 0; i < N; ++i) {
        arr[i] = dis(gen);
    }

    // Sort the array (binary search requires sorted array)
    sort(arr.begin(), arr.end());

    // Display the sorted array
    cout << "Sorted array: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;

    // Input the element to search for
    int target;
    cout << "Enter the number to search for: ";
    cin >> target;

    // Perform binary search
    int result = binarySearch(arr, target);

    // Display result
    if (result != -1) {
        cout << "Element " << target << " found at index " << result << endl;
    } else {
        cout << "Element " << target << " not found in the array" << endl;
    }

    return 0;
}
