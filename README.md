# BinarySearchTreeVisualizer
A Binary Search Tree (BST) is a specialized type of binary tree in which each vertex can have up to two children. This structure adheres to the BST property, stipulating that every vertex in the left subtree of a given vertex must carry a value smaller than that of the given vertex, and every vertex in the right subtree must carry a value larger. 

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
These are the import statements for the required classes and packages, including Swing components (javax.swing) and GUI-related classes (java.awt).


public class BinarySearchTreeVisualizer extends JFrame {
    private static final int WIDTH = 800;
    private static final int HEIGHT = 600;
This class BinarySearchTreeVisualizer extends JFrame, 
meaning it represents a GUI window for visualizing a Binary Search Tree (BST).
The constants WIDTH and HEIGHT represent the dimensions of the window.

private BinarySearchTree bst;
private TreePanel treePanel;
These are instance variables of the BinarySearchTreeVisualizer class.
bst is an instance of the inner class BinarySearchTree, representing the Binary Search Tree data structure.
treePanel is an instance of the inner class TreePanel, representing the visual panel where the BST will be drawn.

public BinarySearchTreeVisualizer() {
    // Constructor - This is the initialization part of the class
    setTitle("Binary Search Tree Visualizer");
    setSize(WIDTH, HEIGHT);
    setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    setLocationRelativeTo(null);
This is the constructor for the BinarySearchTreeVisualizer class.
It sets up the properties of the JFrame window, including its title, size, and default close operation (EXIT_ON_CLOSE).

bst = new BinarySearchTree();
treePanel = new TreePanel(bst);
add(treePanel);
Inside the constructor, a new BinarySearchTree object bst is created, representing an empty Binary Search Tree.
A new TreePanel object treePanel is created, passing the bst as an argument to the constructor. This treePanel is the visual representation of the BST.
The treePanel is added to the JFrame using the add method.

JPanel inputPanel = new JPanel();

JTextField inputField = new JTextField(10);

JButton insertButton = new JButton("Insert");

insertButton.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        // ActionListener for the Insert button
        // Gets the input from the inputField, parses it to an integer, and inserts the value into the BST.
        // Then, repaints the treePanel to update the visualization.
        // Shows an error message if the input is not a valid integer.
    }
});
inputPanel.add(inputField);
inputPanel.add(insertButton);
add(inputPanel, BorderLayout.SOUTH);
In this part, a new JPanel inputPanel is created to hold the input components.
A JTextField inputField with width 10 is created to allow the user to enter values to insert into the BST.
A JButton insertButton with the label "Insert" is created. An action listener is added to the button using an anonymous inner class.
Inside the action listener, the code retrieves the input from inputField, parses it to an integer, and attempts to insert the value into the BST using the insert method of the BinarySearchTree.
If the input is not a valid integer, an error message is shown using JOptionPane.showMessageDialog.
The inputPanel is then added to the JFrame's SOUTH position (at the bottom) using the add method.

setVisible(true);
Finally, the setVisible(true) method is called to make the JFrame visible.


public static void main(String[] args) {
    SwingUtilities.invokeLater(BinarySearchTreeVisualizer::new);
}
This is the main method, which is the entry point of the program.
It invokes the BinarySearchTreeVisualizer constructor using SwingUtilities.invokeLater to ensure the GUI components are created and updated in the event dispatch thread.

private class TreePanel extends JPanel {
This class TreePanel is an inner class of BinarySearchTreeVisualizer, representing the panel for drawing the BST visualization.


private BinarySearchTree bst;
private int nodeSize = 30;
private int levelHeight = 80;
private int initialX;
private int initialY;
These are instance variables of the TreePanel class.
bst is the BinarySearchTree instance that this panel will visualize.
nodeSize represents the size of each node (circle) in the visualization.
levelHeight represents the vertical distance between levels of the BST nodes.
initialX and initialY represent the starting position (top-left corner) of the BST visualization.

public TreePanel(BinarySearchTree bst) {
    this.bst = bst;
    setPreferredSize(new Dimension(WIDTH, HEIGHT));
    initialX = getWidth() / 2;
    initialY = 50;
}
This is the constructor for the TreePanel class.
It sets up the bst instance variable with the given BinarySearchTree instance.
It sets the preferred size of the panel to the specified WIDTH and HEIGHT.
It calculates the initial starting position initialX as half of the panel's width, and initialY as 50 (fixed height).

@Override
protected void paintComponent(Graphics g) {
    super.paintComponent(g);
    int treeWidth = calculateTreeWidth(bst.getRoot());
    initialX = (getWidth() - treeWidth) / 2;
    drawNode(g, bst.getRoot(), 0, initialX, initialY);
}
This method is overridden from JPanel to customize the drawing of the BST visualization.
It first calls super.paintComponent(g) to clear the previous drawings and prepare the panel for new drawings.
It calculates the treeWidth (total width) of the BST using the calculateTreeWidth method.
It sets the initialX position to center the BST visualization based on the total width of the BST and the with of the panel.
It then calls drawNode to start drawing the nodes of the BST recursively, starting from the root node.


private int calculateTreeWidth(BinarySearchTree.Node node) {
    if (node == null) {
        return 0;
    }
    int leftWidth = calculateTreeWidth(node.getLeft());
    int rightWidth = calculateTreeWidth(node.getRight());
    return leftWidth + nodeSize + rightWidth;
}
This private method calculates the total width of the BST starting from the given node.
It uses a recursive approach to calculate the width.
If the node is null (empty), it returns 0.
Otherwise, it calculates the widths of the left and right subtrees recursively, and then adds the nodeSize to the sum to get the total width.

private void drawNode(Graphics g, BinarySearchTree.Node node, int level, int x, int y) {
    // ...
}
This private method drawNode is responsible for drawing a single node of the BST.
It takes the Graphics object g, the current node, the level of the node, and the x and y coordinates where the node should be drawn.
This method is called recursively to draw all nodes and their connections in the BST visualization.
The rest of the code inside the drawNode method is responsible for drawing each node as a red circle, writing the node's value inside the circle, and drawing lines to connect the nodes in the tree. The recursive calls to drawNode are used to draw the left and right subtrees of each node.

The BinarySearchTree class represents the actual Binary Search Tree data structure. It has a Node inner class to represent the nodes of the tree, and methods to insert nodes into the tree.
