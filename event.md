# Java Events

## Keyboard Event respond in Java : Press a key button and move the box in the Java GUI

![](https://raw.githubusercontent.com/Ruslan-Aliyev/Java-Works/master/Illustrations/KeyEvent.PNG)

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Key{

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

class MyJPanel extends JPanel implements KeyListener{

	private Point pos;
	private int size;

	public MyJPanel(){
		pos = new Point(100, 80);
		size = 20;
		addKeyListener(this);
		requestFocusInWindow();
	}

	public void keyPressed(KeyEvent e){
		if(e.getKeyCode()==KeyEvent.VK_UP){
			pos.y-=size;
		}
		else if(e.getKeyCode()==KeyEvent.VK_DOWN){
			pos.y+=size;
		}
		else if(e.getKeyCode()==KeyEvent.VK_LEFT){
			pos.x-=size;
		}
		else if(e.getKeyCode()==KeyEvent.VK_RIGHT){
			pos.x+=size;
		}
		repaint();
	}
	public void keyReleased(KeyEvent e){}
	public void keyTyped(KeyEvent e){}

	public void paintComponent(Graphics g){
		super.paintComponent(g);
		g.drawRect(pos.x-size/2, pos.y-size/2, size, size);

	}
}					
```

## Mouse Event respond in Java : Click at a position in the JPanel see see its coordinates

![](https://raw.githubusercontent.com/Ruslan-Aliyev/Java-Works/master/Illustrations/MouseEvent.PNG)

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Mouse {

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

class MyJPanel extends JPanel implements MouseListener{

	private int mouseX;
	private int mouseY;

	public MyJPanel(){
		mouseX = 100;
		mouseY = 100;
		addMouseListener(this);
	}

	public void mousePressed(MouseEvent e){
		mouseX=e.getX();
		mouseY=e.getY();
		repaint();
	}
	public void mouseReleased(MouseEvent e){}
	public void mouseClicked(MouseEvent e){}
	public void mouseEntered(MouseEvent e){}
	public void mouseExited(MouseEvent e){}

	public void paintComponent(Graphics g){
		super.paintComponent(g);
		g.drawString("("+mouseX+","+mouseY+")", mouseX, mouseY);

	}
}
```
