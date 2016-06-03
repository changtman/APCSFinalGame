package c4;
//© A+ Computer Science  -  www.apluscompsci.com
//Name -
//Date -
//Class -
//Lab  -

import java.awt.Graphics;
import java.awt.Color;
import java.awt.Font;
import java.awt.event.MouseListener;
import java.awt.event.MouseEvent;
import java.awt.Canvas;

public class GameBoard extends Canvas implements MouseListener
{
	private int mouseX, mouseY;
	private boolean mouseClicked, gameOver;
	private int mouseButton, prevMouseButton;
	private Grid board;
	
	private final static int WIDTH=300;
	private final static int HEIGHT=300;
	private final static int SCALE = 50;
	private final static int BOARDSIZE = 6;

	public GameBoard()
	{
		mouseClicked = false;
		mouseX = mouseY = 0;
		mouseButton = 0;
		prevMouseButton = -1;
		
		board = new Grid(BOARDSIZE,BOARDSIZE);
		
		addMouseListener(this);
		setBackground(Color.WHITE);
	}

	public void mouseClicked(MouseEvent e)
	{
		mouseClicked = true;
		mouseX=e.getX();
		mouseY=e.getY();
		mouseButton = e.getButton();
		repaint();
	}

	public void paint(Graphics window)
	{		
		window.setColor(Color.white);
		window.fillRect(0,0,640,480);
		window.setFont(new Font("TAHOMA",Font.BOLD,12));
		window.setColor(Color.BLACK);
		window.drawString("c4", 420,55);
		window.drawString("By: Timothy Chang", 420,85);
		window.drawString("Connect 4 to win", 420,105);
		window.drawString("left mouse click for RED", 420,135);
		window.drawString("right mouse click for BLACK", 420,155);
		
		//add timer to get rid of welcome screen

		window.drawRect(50,50,WIDTH,HEIGHT);
		for(int i = 0; i < 5; i++){
			window.drawRect(100 + i*50,50,WIDTH/6,HEIGHT);
		}
		for(int i = 0; i < 5; i++){
			window.drawRect(50,100 + i*50,WIDTH,HEIGHT/6);
		}
		//window.drawRect(100,50,WIDTH/6,HEIGHT);
		//window.drawRect(50,100,WIDTH,HEIGHT/6);
		
		/*window.drawRect(200,50,WIDTH,HEIGHT);
		window.drawRect(250,50,WIDTH/3,HEIGHT);
		window.drawRect(200,100,WIDTH,HEIGHT/3);
		
		window.drawRect(50,200,WIDTH,HEIGHT);
		window.drawRect(100,200,WIDTH/3,HEIGHT);
		window.drawRect(50,250,WIDTH,HEIGHT/3);
		
		window.drawRect(200,200,WIDTH,HEIGHT);
		window.drawRect(250,200,WIDTH/3,HEIGHT);
		window.drawRect(200,250,WIDTH,HEIGHT/3);*/

		if(mouseClicked)
		{
			markBoard();
			board.drawGrid(window);

			if(determineWinner(window))
			{
				board = new Grid(BOARDSIZE,BOARDSIZE);
				
				setBackground(Color.WHITE);
			}	
			mouseClicked = false;
		}
	}

	public void markBoard()
	{
		if(mouseX>=WIDTH/6&&mouseX<=WIDTH+50&&mouseY>=HEIGHT/6&&mouseY<=HEIGHT+50)
		{
			int r = mouseY/50-1;
			int c = mouseX/50-1;
			Piece piece = (Piece)board.getSpot(r,c);
			//if BUTTON1 was pressed and BUTTON1 was not pressed last mouse press
			if(mouseButton==MouseEvent.BUTTON1&&prevMouseButton!=mouseButton)		//left mouse button pressed
			{
				if(piece==null)
				{
					board.setSpot(r,c,new Piece(5+c*50+50,5+r*50+50,WIDTH/6-10,HEIGHT/6-10,"Red",Color.RED));
				}
				//save the current button pressed to compare to next button pressed
				prevMouseButton=mouseButton;
			}
			//if BUTTON3 was pressed and BUTTON3 was not pressed last mouse press
			if(mouseButton==MouseEvent.BUTTON3&&prevMouseButton!=mouseButton)		//left mouse button pressed
			{
				if(piece==null)
				{
					board.setSpot(r,c,new Piece(5+c*50+50,5+r*50+50,WIDTH/6-10,HEIGHT/6-10,"Black",Color.BLACK));
				}
				//save the current button pressed to compare to next button pressed
				prevMouseButton=mouseButton;
			}		
		}
	}
	
	public boolean determineWinner(Graphics window)
	{
		String winner="";
		for (int r = 0; r<board.getNumRows(); r++)
		{
			for(int c = 0; c<3;c++){
				Piece one = (Piece)board.getSpot(r,c);
				Piece two = (Piece)board.getSpot(r,c+1);
				Piece three = (Piece)board.getSpot(r,c+2);
				Piece four = (Piece)board.getSpot(r,c+3);
			
				if(one==null||two==null||three==null||four==null) continue;
			
				if(one.getName().equals(two.getName())&&one.getName().equals(three.getName())&&one.getName().equals(four.getName()))
				{
					winner=one.getName()+" wins horizontally!";
					break;
				}
			}
		}
		
		//check for vertical winner
		for (int r = 0; r<3;r++)
		{
			for(int c = 0; c<board.getNumCols(); c++){
				Piece one = (Piece)board.getSpot(r,c);
				Piece two = (Piece)board.getSpot(r+1,c);
				Piece three = (Piece)board.getSpot(r+2,c);
				Piece four = (Piece)board.getSpot(r+3,c);
			
				if(one==null||two==null||three==null||four==null) continue;
			
				if(one.getName().equals(two.getName())&&one.getName().equals(three.getName())&&one.getName().equals(four.getName()))
				{
					winner=one.getName()+" wins vertically!";
					break;
				}
			}
		}
		
		for (int r = 0; r<3; r++)
		{
			for(int c = 0; c<3;c++){
				Piece one = (Piece)board.getSpot(r,c);
				Piece two = (Piece)board.getSpot(r+1,c+1);
				Piece three = (Piece)board.getSpot(r+2,c+2);
				Piece four = (Piece)board.getSpot(r+3,c+3);
			
				if(one==null||two==null||three==null||four==null) continue;
			
				if(one.getName().equals(two.getName())&&one.getName().equals(three.getName())&&one.getName().equals(four.getName()))
				{
					winner=one.getName()+" wins diagonally!";
					break;
				}
			}
		}
		
		for (int r = 3; r<6; r++)
		{
			for(int c = 0; c<3;c++){
				Piece one = (Piece)board.getSpot(r,c);
				Piece two = (Piece)board.getSpot(r-1,c+1);
				Piece three = (Piece)board.getSpot(r-2,c+2);
				Piece four = (Piece)board.getSpot(r-3,c+3);
			
				if(one==null||two==null||three==null||four==null) continue;
			
				if(one.getName().equals(two.getName())&&one.getName().equals(three.getName())&&one.getName().equals(four.getName()))
				{
					winner=one.getName()+" wins diagonally!";
					break;
				}
			}
		}
		
		/*if((Piece)board.getSpot(0,0) != null && (Piece)board.getSpot(1,1) != null && (Piece)board.getSpot(2,2) != null){
			if(((Piece) board.getSpot(0,0)).getName().equals(((Piece) board.getSpot(1,1)).getName())&&((Piece)board.getSpot(0,0)).getName().equals(((Piece)board.getSpot(2,2)).getName())){
				winner=((Piece) board.getSpot(0,0)).getName()+" wins diagonally!";
			}
		}
		
		
		if((Piece)board.getSpot(0,2) != null && (Piece)board.getSpot(1,1) != null && (Piece)board.getSpot(2,0) != null){
			if(((Piece) board.getSpot(0,2)).getName().equals(((Piece) board.getSpot(1,1)).getName())&&((Piece)board.getSpot(0,2)).getName().equals(((Piece)board.getSpot(2,0)).getName())){
				winner=((Piece) board.getSpot(0,2)).getName()+" wins diagonally!";
			}
		}*/

		if(winner.indexOf("no name")>-1){
		   board.drawGrid(window);
		   return false;
		}
		else if(board.drawGrid(window)&&winner.length()==0){
		   winner =  "cat's game - no winner!\n\n";
		}
				
		if(winner.length()>0)
		{
			window.setFont(new Font("TAHOMA",Font.BOLD,22));
			window.setColor(Color.BLACK);
			window.drawString(winner, 400,250);	
			try{
			   Thread.currentThread().sleep(1500);
			}
			catch(Exception e){
			}
			repaint();
			return true;
		}
		return false;
	}

	public void mouseEntered(MouseEvent e) { }
	public void mouseExited(MouseEvent e) { }
	public void mousePressed(MouseEvent e) { }
	public void mouseReleased(MouseEvent e) { }
}