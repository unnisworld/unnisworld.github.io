---
layout: post
title:  "Binary Tree Inorder Traversal"
date:   2020-04-20
categories: BinaryTree
---

Recursive Solution is very simple

{% highlight java %}
// Recursive function to perform in-order traversal of the tree
public static void inorder(TreeNode root)
{
    // return if the current node is empty
    if (root == null) {
        return;
    }

    // Traverse the left subtree
    inorder(root.left);

    // Display the data part of the root (or current node)
    System.out.print(root.data + " ");

    // Traverse the right subtree
    inorder(root.right);
}
{% endhighlight %}

Iterative Solution requires an explicit Stack.

{% highlight java %}
import java.util.Stack;

// Data structure to store a Binary Tree node
class Node
{
    int data;
    Node left, right;

    // Function to create a new binary tree node having given key
    public Node(int key)
    {
        data = key;
        left = right = null;
    }
};

class Main
{
    // Iterative function to perform in-order traversal of the tree
    public static void inorderIterative(Node root)
    {
        // create an empty stack
        Stack<Node> stack = new Stack();

        // start from root node (set current node to root node)
        Node curr = root;

        // if current node is null and stack is also empty, we're done
        while (!stack.empty() || curr != null)
        {
            // if current node is not null, push it to the stack (defer it)
            // and move to its left child
            if (curr != null)
            {
                stack.push(curr);
                curr = curr.left;
            }
            else
            {
                // else if current node is null, we pop an element from the stack,
                // print it and finally set current node to its right child
                curr = stack.pop();
                System.out.print(curr.data + " ");

                curr = curr.right;
            }
        }
    }

    public static void main(String[] args)
    {
        /* Construct below tree
                  1
                /   \
               /     \
              2       3
             /       / \
            /       /   \
           4       5     6
                  / \
                 /   \
                7     8
        */

        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.right.left = new Node(5);
        root.right.right = new Node(6);
        root.right.left.left = new Node(7);
        root.right.left.right = new Node(8);

        inorderIterative(root);
    }
}

{% endhighlight %}

[link]: https://www.techiedelight.com/inorder-tree-traversal-iterative-recursive/
