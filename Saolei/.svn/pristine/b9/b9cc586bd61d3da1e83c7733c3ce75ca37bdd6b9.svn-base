package com.qinke;

import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Container;
import java.awt.Frame;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Random;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JOptionPane;

public class Saolei implements ActionListener {

	JFrame frame = new JFrame("扫雷游戏");
	JButton reset = new JButton("重来");
	Container container = new Container();
	Saoleic c=new Saoleic();
	// 任务3数据结构
	final int row = c.row;
	final int col = c.col;
	final int leiCount = c.leiCount;
	JButton[][] buttons = new JButton[row][col];
	int[][] counts = new int[row][col];
	final int LEICODE = c.LEICODE;

	public static void main(String[] args) {
		Saolei lei = new Saolei();
	}

	public Saolei() {
		// 任務一:设置可视化界面
		frame.setSize(1000, 1000);
		frame.setResizable(false);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		frame.setLayout(new BorderLayout());
		// 任务二:添加reset按钮
		addResetButton();
		// 任务四:添加button
		addButton();
		// 任务六:埋雷
		addLei();
		// 任务七:添加雷的计数
		calcNeiboLei();
		frame.setVisible(true);
	}

	public void calcNeiboLei() {
		int count;
		for (int i = 0; i < row; i++) {
			for (int j = 0; j < col; j++) {
				count = 0;
				if (counts[i][j] == LEICODE)
					continue;
				if (i > 0 && j > 0 && counts[i - 1][j - 1] == LEICODE)
					count++;
				if (i > 0 && counts[i - 1][j] == LEICODE)
					count++;
				if (i > 0 && j < 19 && counts[i - 1][j + 1] == LEICODE)
					count++;
				if (j > 0 && counts[i][j - 1] == LEICODE)
					count++;
				if (j < 19 && counts[i][j + 1] == LEICODE)
					count++;
				if (i < 19 && j > 0 && counts[i + 1][j - 1] == LEICODE)
					count++;
				if (i < 19 && counts[i + 1][j] == LEICODE)
					count++;
				if (i < 19 && j < 19 && counts[i + 1][j + 1] == LEICODE)
					count++;
				counts[i][j] = count;
				// buttons[i][j].setText(counts[i][j]+"");
			}
		}
	}

	public void addButton() {

		// frame.add(container,BorderLayout.CENTER);
		frame.add(container, BorderLayout.CENTER);
		container.setLayout(new GridLayout(row, col));
		for (int i = 0; i < row; i++) {
			for (int j = 0; j < col; j++) {
				JButton button = new JButton();
				button.setBackground(Color.white);
				button.setOpaque(true);
				// 任务五添加点击驱动
				button.addActionListener(this);
				buttons[i][j] = button;
				container.add(button);
			}
		}
	}

	public void addLei() {
		Random rand = new Random();
		int randRow, randCol;

		for (int i = 0; i < leiCount; i++) {
			randRow = rand.nextInt(row);
			randCol = rand.nextInt(col);
			if (counts[randRow][randCol] == LEICODE) {
				i--;
			} else {
				counts[randRow][randCol] = LEICODE;
				// buttons[randRow][randCol].setText("X");
			}
		}
	}

	public void addResetButton() {
		reset.setBackground(Color.green);
		reset.setOpaque(true);
		reset.addActionListener(this);
		frame.add(reset, BorderLayout.NORTH);
	}

	public void loseGame() {
		for (int i = 0; i < row; i++) {
			for (int j = 0; j < col; j++) {
				int count = counts[i][j];
				if (count == LEICODE) {
					buttons[i][j].setText("X");
					buttons[i][j].setEnabled(false);
				} else {
					buttons[i][j].setText(count + "");
					buttons[i][j].setEnabled(false);
				}
			}
		}
	}

	public void openCell(int i, int j) {
		if (buttons[i][j].isEnabled() == false)
			return;

		//buttons[i][j].setEnabled(false);

		if (counts[i][j] == 0) {
			if (i > 0 && j > 0 && counts[i - 1][j - 1] == LEICODE)
				openCell(i - 1, j - 1);
			if (i > 0 && counts[i - 1][j] != LEICODE)
				openCell(i - 1, j);
			if (i > 0 && j < 19 && counts[i - 1][j + 1] != LEICODE)
				openCell(i - 1, j + 1);
			if (j > 0 && counts[i][j - 1] != LEICODE)
				openCell(i, j - 1);
			if (j < 19 && counts[i][j + 1] != LEICODE)
				openCell(i, j + 1);
			if (i < 19 && j > 0 && counts[i + 1][j - 1] != LEICODE)
				openCell(i + 1, j - 1);
			if (i < 19 && counts[i + 1][j] == LEICODE)
				openCell(i + 1, j);
			if (i < 19 && j < 19 && counts[i + 1][j + 1] != LEICODE)
				openCell(i + 1, j + 1);
		} else {
			buttons[i][j].setText(counts[i][j] + "");
			buttons[i][j].setBackground(Color.YELLOW);
		}
	}

	public void checkWin() {
		for (int i = 0; i < row; i++) {
			for (int j = 0; j < col; j++) {
				if (buttons[i][j].isEnabled() == true && counts[i][j] != LEICODE)
					return;

			}
		}
		JOptionPane.showMessageDialog(frame, "你赢了！");
	}

	@Override
	public void actionPerformed(ActionEvent e) {
		// reset.setBackground(Color.green);
		JButton button = (JButton) e.getSource();
		if (button.equals(reset)) {
			for (int i = 0; i < row; i++) {
				for (int j = 0; j < col; j++) {
					buttons[i][j].setText("");
					buttons[i][j].setEnabled(true);
					buttons[i][j].setBackground(Color.yellow);
					counts[i][j] = 0;
				}
			}
			addLei();
			calcNeiboLei();
		} else {
			int count = 0;
			for (int i = 0; i < row; i++) {
				for (int j = 0; j < col; j++) {
					if (button.equals(buttons[i][j])) {
						count = counts[i][j];
						if (count == LEICODE) {
							loseGame();
						} else {
							openCell(i, j);
							checkWin();
						}
						return;
					}
				}
			}

			button.setText("0");
			button.setEnabled(false);
		}
	}
}
