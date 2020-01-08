# Java Animation

![](https://raw.githubusercontent.com/Ruslan-Aliyev/Java-Works/master/Illustrations/javaAnim.PNG)

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Anim {

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

	private Timer t;
	private Point[] thePoints;

	public MyJPanel(){
		thePoints = new Point[100];
		for(int i=0; i&lt;thePoints.length;i++){thePoints[i]=new Point(150,150);}

		t=new Timer(30, this);
		t.start();
	}

	public void actionPerformed(ActionEvent e){
		for(int i=0; i&lt;thePoints.length;i++){
			int dX=(int)(Math.random()*5)-2;
			int dY=(int)(Math.random()*5)-2;
			thePoints[i].translate(dX, dY);
		}
		repaint();
	}

	public void paintComponent(Graphics g){
		super.paintComponent(g);
		for(int i=0; i&lt;thePoints.length;i++){
			g.drawOval(thePoints[i].x-3, thePoints[i].y-3, 6,6);
		}

	}
}				
```
