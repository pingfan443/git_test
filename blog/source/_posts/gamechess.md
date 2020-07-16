---
title: 五子棋
date: 2020-07-04 19:27:00
tags: 五子棋游戏
category: java
index_img: https://cdn.jsdelivr.net/gh/pingfan443/blog-imgs/imgs/20200715161436.jpg
---

# 五子棋

界面：

<img src="https://cdn.jsdelivr.net/gh/pingfan443/blog-imgs/imgs/20200715155425.png" style="zoom:50%;" />

## 特色：

有八张棋盘图片和十张棋子图片供选择

<img src="https://cdn.jsdelivr.net/gh/pingfan443/blog-imgs/imgs/20200715155921.png" style="zoom: 50%;" />

排行榜的信息

![](https://cdn.jsdelivr.net/gh/pingfan443/blog-imgs/imgs/20200715160305.png)

## 类名

### Wymain.java

> 棋盘的窗体，以及监听事件

```java
package game2;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Random;

import javax.swing.JFrame;
import javax.swing.JMenu;
import javax.swing.JMenuBar;
import javax.swing.JMenuItem;
import javax.swing.JOptionPane;

public class Wumain extends JFrame{
	/**
	 * 
	 */	
	pan p = null;//棋盘
	JMenuBar menuber = new JMenuBar();//菜单栏
	JMenu jm1 = new JMenu("选项");//菜单
	JMenu jm2 = new JMenu("设置");
	JMenu jm3 = new JMenu("帮助");
	JMenuItem jm1_1 = new JMenuItem("重新开始");//菜单项
	JMenuItem jm1_2 = new JMenuItem(" 排行榜");
	JMenuItem jm1_3 = new JMenuItem("退出游戏");
	JMenuItem jm2_1 = new JMenuItem("更换棋盘");
	JMenuItem jm2_2 = new JMenuItem("更换棋子");
	JMenuItem jm3_1 = new JMenuItem("关于我们");
	public Wumain()
	{
		   p =new pan();
		   this.setSize(585,600);//设置窗体大小
		   this.setLocation(200,100);//设窗体位置
		   this.add(p);//默认添加到中间
		   this.setResizable(false);//设置此窗体是否可由用户调整大小。
		   this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);// 设置用户在此窗体上发起 "close" 时默认执行的操作
		   jm1.add(jm1_1);
		   jm1.add(jm1_2);
		   jm1.add(jm1_3);
		   jm2.add(jm2_1);
		   jm2.add(jm2_2);
		   jm3.add(jm3_1);
		   menuber.add(jm1);
		   menuber.add(jm2);
		   menuber.add(jm3); 
		   this.setJMenuBar(menuber);//设置此窗体的菜单栏。
		   this.addMouseListener(p);//给面板添加监听事件
		   jm1_1.addActionListener(new ActionListener() {//重新开始的监听事件
				
			@Override
			public void actionPerformed(ActionEvent e) {
				for(int i=0;i<p.row;i++){
					for(int j=0;j<p.col;j++){
						p.num[i][j] = 0;
					}
				}
				p.canSetqizi = true;
				p.qizi_num = 0;
				repaint();//重绘此组件。
			}
		});
		   jm1_2.addActionListener(new ActionListener() {//排行榜监听事件
				
			   public void actionPerformed(ActionEvent e) {
			String msg ="排行榜\n" +
					"局数      步数      结果\n";
			for(int i=0;i<p.paihanglist.size();i++)
			{
				paihangbang ph = p.paihanglist.get(i);
			      msg = msg+"   "+ph.getJushu()
			    		  +"          "+ph.getBushu()
			    		  +"          "+ph.getJieguo()+"\n";
			}
				JOptionPane.showMessageDialog(null, msg);//显示消息
			   }
		});
		   jm1_3.addActionListener(new ActionListener() {//退出游戏菜单项的监听事件
//			匿名虚构类
			@Override
			public void actionPerformed(ActionEvent e) {
				System.exit(0);//退出即可
				
			}
		});

		   jm2_1.addActionListener(new ActionListener() {//更换棋盘
			
			@Override
			public void actionPerformed(ActionEvent e) {
				Random r = new Random();
				int n = r.nextInt(8);//产生[0,8)的随机数左闭右开
				String qipan_name = "qipan"+n+".jpg";
				p.qipan_name = qipan_name;
				repaint();
			}
		});
		   jm2_2.addActionListener(new ActionListener() {//更换棋子
			
			@Override
			public void actionPerformed(ActionEvent e) {
				Random r = new Random();
				int n = r.nextInt(8);//产生[0,8)的随机数左闭右开
				String qizi1_name = "c"+n+".png";//产生的n是[0,8)的随机数
				String qizi2_name = "c"+(n+1)+".png";//这里设置n+1一方面是避免两个
				//棋子一样，另一方面棋子有8这个图片所以n=7时，会产生8这张图片，避免了8这张图片不存在的现象
				p.qizi1_name = qizi1_name;
				p.qizi2_name = qizi2_name;	
				repaint();
			}
		});
		   jm3_1.addActionListener(new ActionListener() {//关于我们，这里就是简单的游戏介绍
			
			@Override
			public void actionPerformed(ActionEvent e) {
				String msg ="关于我们\n" +
						"1、玩家先落子;\n" +
						"2、形成5颗同色连子即为赢;\n\n\n" +
						"     制作人：王豪杰";
				JOptionPane.showMessageDialog(null, msg);
				
			}
		});
		   this.setVisible(true);//显示该窗体，必须有这句话
	}
	public static void main(String[] args){
		Wumain w = new Wumain();
	}
}

```



### pan.java

> 棋盘的面板，该棋盘核心代码：当我方下够超过3个以上构成直线棋子，对方就会进行围堵。

```java
package game2;

import java.awt.Graphics;
import java.awt.Image;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;
import java.util.ArrayList;
import java.util.List;
import java.util.Locale;
import java.util.Random;

import javax.swing.ImageIcon;
import javax.swing.JOptionPane;
import javax.swing.JPanel;

public class pan extends JPanel implements MouseListener{
	/**
	 * 
	 */
	int i=0,j=0;
	int row = 15;
//	数组下标
	int col = 15;
//	数组上标
	String qipan_name = "qipan1.jpg";
	String qizi1_name = "c1.png";
	String qizi2_name = "c2.png";
	int num[][] = new int[row][col];
//	0：标示该位置为空，1：标示红棋子，2：标示黑棋子
	boolean canSetqizi = true;//定义boolean值，用来判断该位置是否有子
	int qizi_num = 0;//	定义记录落子数
	List<paihangbang> paihanglist = new ArrayList<paihangbang>();//	定义集合，用来存储排行榜
	public void paint(Graphics g){//在这个面板中绘制图案，在界面进行刷新时就会被调用。
		super.paint(g);
		Image img= new ImageIcon("img/"+qipan_name).getImage();
//		调入棋盘图片，首先加载图片
		g.drawImage(img, 0, 0, 567, 567, this);// 绘制指定图像中已缩放到适合指定矩形内部的图像。
//		绘制棋盘
		Image c1= new ImageIcon("img/"+qizi1_name).getImage();//getImage()方法：返回此图标的 Image。
		Image c2= new ImageIcon("img/"+qizi2_name).getImage();
		for(int i = 0;i<num.length;i++){
			for(int j = 0;j<num[i].length;j++){
				if(num[i][j] == 1)
				{
					g.drawImage(c1, i*35+20, j*35+20, 35, 35, this);//其实就是画个图片
					//绘制指定图像中已缩放到适合指定矩形内部的图像。c1:棋子图案，然后是坐标，大小，和通知对象
				}
				else if(num[i][j] == 2)
				{
					g.drawImage(c2, i*35+20, j*35+20, 35, 35, this);
				}
			}
//			重绘棋子
		}
//		重载整个界面（防止最小化后原内容丢失）
	}
	public int[] getLoc(int x,int y) {//这个就是当你的棋子数在水平方向，竖直方向，或者斜方向的棋子数>3,
		//对方会判断有危险，就会堵你，这个就是核心所在
		int count = 1;
//		定义计数器，用于计算棋子数
		int[] wz1 = null;
		int[] wz2 = null;
//		定义数组，用来存储危险位置
		for(int i =x-1;i>=0;i--){
			if(num[i][y] == num[x][y])
			{
				count++;
			}
			else
			{
				if(num[i][y] == 0){
					wz1 = new int[]{i,y};
//					获取左边的危险位置坐标
				}
				break;
			}
		}
//		左
		for(int i =x+1;i<row;i++){
			if(num[i][y] == num[x][y])
			{
				count++;
			}else{
				if(num[i][y] == 0){
					wz2 = new int[]{i,y};
//					获取右边位置危险坐标
				}
				break;
			}
		}
//		右
		if(count>=3)
		{
			if(wz1 != null){
				return wz1;
//				判断返回左边危险位置
			}else if(wz2 != null){
				return wz2;
//				判断返回右边危险位置
			}else{
				return null;
			}
		}
//		左右
		count = 1;
		wz1 = null;
		wz2 = null;
//		初始化所有参数
		for(int j =y-1;j>=0;j--){
			if(num[x][j] == num[x][y])
			{
				count++;
			}
			else
			{
				if(num[x][j] == 0){
					wz1 = new int[]{x,j};
				}
				break;
			}
		}
//		上
		for(int j =y+1;j<col;j++){
			if(num[x][j] == num[x][y])
			{
				count++;
			}else{
				if(num[x][j] == 0){
					wz2 = new int[]{x,j};
				}
				break;
			}
		}
//		下
		if(count>=3)
		{
			if(wz1 != null){
				return wz1;
			}else if(wz2 != null){
				return wz2;
			}else{
				return null;
			}
		}
//		上下
		count = 1;
		wz1 = null;
		wz2 = null;
		for(int i =x-1,j =y-1;i>=0&&j>=0;i--,j--){
			if(num[i][j] == num[x][y])
			{
				count++;
			}
			else
			{
				if(num[i][j] == 0){
					wz1 = new int[]{i,j};
				}
				break;
			}
		}
//		左上
		for(int i =x+1,j =y+1;i<row&&j<col;i++,j++){
			if(num[i][j] == num[x][y])
			{
				count++;
			}else{
				if(num[i][j] == 0){
					wz2 = new int[]{i,j};
				}
				break;
			}
		}
//		右下
		if(count>=3)
		{
			if(wz1 != null){
				return wz1;
			}else if(wz2 != null){
				return wz2;
			}else{
				return null;
			}
		}
//		左上右下
		count = 1;
		wz1 = null;
		wz2 = null;
		for(int i =x-1,j =y+1;i>=0&&j<col;i--,j++){
			if(num[i][j] == num[x][y])
			{
				count++;
			}
			else
			{
				if(num[i][j] == 0){
					wz1 = new int[]{i,j};
				}
				break;
			}
		}
//		左下
		for(int i =x+1,j =y-1;i<row&&j>=0;i++,j--){
			if(num[i][j] == num[x][y])
			{
				count++;
			}else{
				if(num[i][j] == 0){
					wz2 = new int[]{i,j};
				}
				break;
			}
		}
//		右上
		if(count>=3)
		{
			if(wz1 != null){
				return wz1;
			}else if(wz2 != null){
				return wz2;
			}else{
				return null;
			}
		}
//		左下右上
		return null;
	}
	public boolean iswin(int x,int y){//判断是否赢
		int count = 1;
		for(int i =x-1;i>=0;i--){
			if(num[i][y] == num[x][y])
			{
				count++;
			}
			else
			{
				break;
			}
		}
//		左
		for(int i =x+1;i<row;i++){
			if(num[i][y] == num[x][y])
			{
				count++;
			}else{
				break;
			}
		}
//		右
		if(count>=5)
		{
			return true;
		}
//		左右
		count = 1;
		for(int j =y-1;j>=0;j--){
			if(num[x][j] == num[x][y])
			{
				count++;
			}
			else
			{
				break;
			}
		}
//		上
		for(int j =y+1;j<col;j++){
			if(num[x][j] == num[x][y])
			{
				count++;
			}else{
				break;
			}
		}
//		下
		if(count>=5)
		{
			return true;
		}
//		上下
		count = 1;
		for(int i =x-1,j =y-1;i>=0&&j>=0;i--,j--){
			if(num[i][j] == num[x][y])
			{
				count++;
			}
			else
			{
				break;
			}
		}
//		左上
		for(int i =x+1,j =y+1;i<row&&j<col;i++,j++){
			if(num[i][j] == num[x][y])
			{
				count++;
			}else{
				break;
			}
		}
//		右下
		if(count>=5)
		{
			return true;
		}
//		左上右下
		count = 1;
		for(int i =x-1,j =y+1;i>=0&&j<col;i--,j++){
			if(num[i][j] == num[x][y])
			{
				count++;
			}
			else
			{
				break;
			}
		}
//		左下
		for(int i =x+1,j =y-1;i<row&&j>=0;i++,j--){
			if(num[i][j] == num[x][y])
			{
				count++;
			}else{
				break;
			}
		}
//		右上
		if(count>=5)
		{			
			return true;
		}
//		左下右上
		return false;
	}
//	判断输赢
	@Override
	public void mouseClicked(MouseEvent e) {// 鼠标按键在组件上单击（按下并释放）时调用
		if(canSetqizi){
			Graphics g = this.getGraphics();//为组件创建一个图形上下文。如果组件当前是不可显示的，则此方法返回 null。
			int checkusersuccess = 0;//标示是否落子成功
			int x = e.getX();//返回事件相对于源组件的水平 x 坐标。
			int y = e.getY();//返回事件相对于源组件的垂直 y 坐标。
//			获取鼠标点击的位置
			Image c1= new ImageIcon("img/"+qizi1_name).getImage();
			int i = (x-25)/35;//减去行数多余的部分，/35就是获取的行数
			int j = (y-75)/35;//减去列数多余的部分，/35就是获取的列数
			//i，j就是获取棋子的坐标
			if(num[i][j] != 0){//因为1代表红棋，2代表黑棋，所以!=0就是该位置已经存在棋，不能再下
	             JOptionPane.showMessageDialog(null, "该位置有旗子，请重新落子");
	             return;
//	             判断有子，终止本次事件，进行下次事件触发
			}else{
				g.drawImage(c1, i*35+20, j*35+20, 35, 35, this);
//				画出玩家落子
				num[i][j] = 1;
//				给数组付一个只值，表示该位置有旗子
				checkusersuccess = 1;//代表落子成功
//				标示量标示
				qizi_num++;
//				记录玩家落子步数
			}
			boolean b=iswin(i,j);
			if(b){
				JOptionPane.showMessageDialog(null, "你赢了！");
				canSetqizi = false;
				paihangbang ph = new paihangbang();
				ph.setJushu(paihanglist.size()+1);
				ph.setBushu(qizi_num);//棋子步数
				ph.setJieguo("win");//结果状态
				paihanglist.add(ph);
				return;
			}
//			调用boolean判断方法
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e1) {
				e1.printStackTrace();
			}
//			时间间隔：玩家落子后的等待
			Random r = new Random();
			Image c2 = new ImageIcon("img/"+qizi2_name).getImage();
//			调入黑棋子图片
			do{
				int[] wz =getLoc(i, j);
				if(wz == null){
			i = r.nextInt(15);
			j = r.nextInt(15);
				}else{
					i=wz[0];
					j=wz[1];
				}
//			设置随机的坐标
			}while(num[i][j] != 0);
			g.drawImage(c2, i*35+20, j*35+20, 35, 35, this);
			num[i][j] = 2;
			boolean d=iswin(i,j);
			if(d){
				JOptionPane.showMessageDialog(null, "你输了！");
				canSetqizi = false;
				paihangbang ph = new paihangbang();
				ph.setJushu(paihanglist.size()+1);
				ph.setBushu(qizi_num);
				ph.setJieguo("fail");
				paihanglist.add(ph);
				return;
			}
//			随机电脑落子位置;	
		}
	}

	@Override
	public void mousePressed(MouseEvent e) {//鼠标按键在组件上按下时调用。
		// TODO Auto-generated method stub
		
	}

	@Override
	public void mouseReleased(MouseEvent e) {//鼠标按钮在组件上释放时调用。
		// TODO Auto-generated method stub
		
	}

	@Override
	public void mouseEntered(MouseEvent e) {//鼠标进入到组件上时调用。
		// TODO Auto-generated method stub
		
	}

	@Override
	public void mouseExited(MouseEvent e) {// 鼠标离开组件时调用。
		// TODO Auto-generated method stub
		
	}
		
}

```



### paihangbang.java

> 封装了排行榜中的数据

```java
package game2;

public class paihangbang {
	
	private int jushu;
	private int bushu;
	private String jieguo;
	public int getJushu() {
		return jushu;
	}
	public void setJushu(int jushu) {
		if(jushu<1){
			this.jushu = 1;
		}
		this.jushu = jushu;
	}
	public int getBushu() {
		return bushu;
	}
	public void setBushu(int bushu) {
		this.bushu = bushu;
	}
	public String getJieguo() {
		return jieguo;
	}
	public void setJieguo(String jieguo) {
		this.jieguo = jieguo;
	}
}

```

源码及其图片资源：

```c++
链接：https://pan.baidu.com/s/1vr6koVFQUF83Hg5RLNPj7Q 
提取码：2bfy
```

