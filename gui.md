# Java GUI

## Sum calculator in Java

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class GUI {

	public static void main(String[] args) {

		String fn = JOptionPane.showInputDialog("Enter 1st number: ");
		String sn  = JOptionPane.showInputDialog("Enter 2nd  number: ");

		int num1 = Integer.parseInt(fn);
		int num2 = Integer.parseInt(sn);

		int sum = num1+num2;
		JOptionPane.showMessageDialog(null, "Answer: "+sum, "Sum", JOptionPane.PLAIN_MESSAGE);

	}
}				
```

### String concatenator in Java : Set button joins the 2 strings, Random button just prints something random

![](https://raw.githubusercontent.com/Ruslan-Aliyev/Java-Works/master/Illustrations/JavaButtons.PNG)

```java	
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class GUI {

	public static void main(String[] args) {
		MyJFrame gui = new MyJFrame ("MyWindow", 100, 100, 200, 200);
	}
}

class MyJFrame extends JFrame{

	public MyJFrame (String title, int x, int y, int width, int height){
		setTitle(title);
		setLocation(x, y);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		MyJPanel frameContent = new MyJPanel();
		Container visibleArea = getContentPane();
		visibleArea.add(frameContent);
		frameContent.setPreferredSize(new Dimension(width, height));
		pack();
		frameContent.requestFocusInWindow();
		setVisible(true);
		
	}
}

class MyJPanel extends JPanel implements ActionListener{

	private JTextField name1;
	private JTextField name2;
	private JTextField name;
	private JButton set;
	private JButton random;

	public MyJPanel(){
		name1 = new JTextField("First name is "); 
		name2 = new JTextField("Last name is ");
		name = new JTextField(15);
		set = new JButton("Set");
		random = new JButton("Random");
		add(name1);
		add(name2);
		add(name);
		add(set);
		add(random);
		name1.addActionListener(this);
		name2.addActionListener(this);
		set.addActionListener(this);
		random.addActionListener(this);
	}
	public void actionPerformed(ActionEvent e){
		if (e.getSource()==set){
			String first = name1.getText();
			String second = name2.getText();
			name.setText(first+second);
		} if (e.getSource()==random) {
			name.setText("Random...");
		}
	}
}					
```
					
## Drawing shapes in Java

![](https://raw.githubusercontent.com/Ruslan-Aliyev/Java-Works/master/Illustrations/drawingThings.PNG)

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class GUI {

	public static void main(String[] args) {
		MyJFrame gui = new MyJFrame ("MyWindow", 100, 100, 200, 200);
	}
}

class MyJFrame extends JFrame{

	public MyJFrame (String title, int x, int y, int width, int height){
		setTitle(title);
		setLocation(x, y);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		MyJPanel frameContent = new MyJPanel();
		Container visibleArea = getContentPane();
		visibleArea.add(frameContent);
		frameContent.setPreferredSize(new Dimension(width, height));
		pack();
		frameContent.requestFocusInWindow();
		setVisible(true);
		
	}
}

class MyJPanel extends JPanel{

	private Circle[] circles;

	public MyJPanel(){
		circles = new Circle[2];
		circles [0] = new Circle(50, 200, 150);
		circles [1] = new Circle(10, 30, 100);
	}

	public void paintComponent(Graphics g){
		super.paintComponent(g);

		g.setColor(Color.BLUE);
		g.fillOval(40, 60, 80, 80);

		g.drawRect(80, 60, 80, 80);

		for (int i=0; i&lt;circles.length; i++){
			circles[i].draw(g);
		}
	}
}

class Circle {
	private int radius;
	private int xCentre;
	private int yCentre;

	public Circle(int r, int x, int y){
		radius = r;
		xCentre = x;
		yCentre = y;
	}

	public void draw(Graphics g){
		g.drawOval (xCentre - radius, yCentre - radius, 2*radius, 2*radius);
	}
}				
```
