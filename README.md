# Week-8
#include <iostream>
#include <string>
using namespace std;

// TreeNode class definition
class TreeNode {
public:
    string gender;
    int marks;
    TreeNode* left;
    TreeNode* right;

    // Constructor
    TreeNode(int m, string g) {
        marks = m;
        gender = g;
        left = right = nullptr;
    }
};

// BST class definition
class BST {
private:
    TreeNode* root;

    // Helper function for inserting into BST
    TreeNode* insert(TreeNode* node, int marks, string gender) {
        if (node == nullptr) {
            return new TreeNode(marks, gender);
        }
        if (marks < node->marks) {
            node->left = insert(node->left, marks, gender);
        } else {
            node->right = insert(node->right, marks, gender);
        }
        return node;
    }

    // Helper function for in-order traversal
    void inorder(TreeNode* node) {
        if (node == nullptr) return;
        inorder(node->left);
        cout << "(" << node->marks << ", " << node->gender << ")" << endl;
        inorder(node->right);
    }

public:
    // Constructor
    BST() {
        root = nullptr;
    }

    // Function to insert nodes into the BST
    void insert(int marks, string gender) {
        root = insert(root, marks, gender);
    }

    // Function for in-order traversal
    void inorder() {
        inorder(root);
    }
};

int main() {
    // Sample data from the task
    int marks[] = {10, 5, 14, 3, 7, 9, 18, 15, 17, 100};
    string gender[] = {"Female", "Male", "Male", "Male", "Male", "Female", "Female", "Female", "Female", "Male"};

    BST maleBST, femaleBST;
    bool bstCreated = false;

    int choice;
    do {
        cout << "Given Data\n";
        cout << "Marks: ";
        for (int i = 0; i < 10; i++) {
            cout << marks[i] << " ";
        }
        cout << "\nGender: ";
        for (int i = 0; i < 10; i++) {
            cout << gender[i] << " ";
        }
        cout << "\n\nEnter your choice\n";
        cout << "1 to create BSTs\n";
        cout << "2 to see Male students BST\n";
        cout << "3 to see Female students BST\n";
        cout << "0 to terminate the program\n";
        cin >> choice;

        switch (choice) {
            case 1:
                if (!bstCreated) {
                    cout << "BST of male students is being created...\n";
                    for (int i = 0; i < 10; ++i) {
                        if (gender[i] == "Male") {
                            maleBST.insert(marks[i], gender[i]);
                        }
                    }
                    cout << "Done\n";

                    cout << "BST of female students is being created...\n";
                    for (int i = 0; i < 10; ++i) {
                        if (gender[i] == "Female") {
                            femaleBST.insert(marks[i], gender[i]);
                        }
                    }
                    cout << "Done\n";
                    bstCreated = true;
                } else {
                    cout << "BSTs are already created.\n";
                }
                break;
            case 2:
                if (bstCreated) {
                    cout << "In Order Traversal of Male students BST\n";
                    maleBST.inorder();
                } else {
                    cout << "Please create the BSTs first.\n";
                }
                break;
            case 3:
                if (bstCreated) {
                    cout << "In Order Traversal of Female students BST\n";
                    femaleBST.inorder();
                } else {
                    cout << "Please create the BSTs first.\n";
                }
                break;
            case 0:
                cout << "Program terminated.\n";
                break;
            default:
                cout << "Invalid choice. Please enter again.\n";
                break;
        }

    } while (choice != 0);

    return 0;
}
