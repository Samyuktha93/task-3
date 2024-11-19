import java.awt.Color;
import java.awt.Graphics;
import java.awt.Point;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyAdapter;
import java.awt.event.KeyEvent;
import java.util.ArrayList;

import javax.swing.JFrame;
import javax.swing.JOptionPane;
import javax.swing.Timer;
public class SnakeGame extends JFrame
{
    private final int WIDTH = 800;
    private final int HEIGHT = 600;
    private final int UNIT_SIZE = 20;
    private final int GAME_UNITS = (WIDTH * HEIGHT) / UNIT_SIZE;
    private final int DELAY = 100;
    private ArrayList<Point> snake;
    private Point food;
    private char direction = 'R';
    private boolean running = false;
    private Timer timer;
    public SnakeGame()
    {
        setTitle("Snake Game");
        setSize(WIDTH, HEIGHT);
        setResizable(false);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        setVisible(true);
        snake = new ArrayList<>();
        snake.add(new Point(UNIT_SIZE, UNIT_SIZE));
        spawnFood();
        timer = new Timer(DELAY, new ActionListener()
        {
            @Override
            public void actionPerformed(ActionEvent e)
            {
                if (running)
                {
                    move();
                    checkFoodCollision();
                    checkSelfCollision();
                    repaint();
                }
            }
        });
        addKeyListener(new KeyAdapter()
        {
            @Override
            public void keyPressed(KeyEvent e)
            {
                switch (e.getKeyCode())
                {
                    case KeyEvent.VK_UP:
                        if (direction != 'D') direction = 'U';
                        break;
                    case KeyEvent.VK_DOWN:
                        if (direction != 'U') direction = 'D';
                        break;
                    case KeyEvent.VK_LEFT:
                        if (direction != 'R') direction = 'L';
                        break;
                    case KeyEvent.VK_RIGHT:
                        if (direction != 'L') direction = 'R';
                        break;
                    case KeyEvent.VK_SPACE:
                        if (!running)
                        {
                            startGame();
                        }
                        break;
                }
            }
        });
        // Display instructions and wait for space to start
        JOptionPane.showMessageDialog(this, "Press SPACE to start the game", "Snake Game", JOptionPane.INFORMATION_MESSAGE);
    }
    private void startGame()
    {
        running = true;
        snake.clear();
        snake.add(new Point(UNIT_SIZE, UNIT_SIZE));
        direction = 'R';
        spawnFood();
        timer.start();
    }
    private void spawnFood()
    {
        int x = (int) (Math.random() * (WIDTH / UNIT_SIZE)) * UNIT_SIZE;
        int y = (int) (Math.random() * (HEIGHT / UNIT_SIZE)) * UNIT_SIZE;
        food = new Point(x, y);
    }
    private void move()
    {
        Point head = new Point(snake.get(0));
        switch (direction)
        {
            case 'U':
                head.y -= UNIT_SIZE;
                break;
            case 'D':
                head.y += UNIT_SIZE;
                break;
            case 'L':
                head.x -= UNIT_SIZE;
                break;
            case 'R':
                head.x += UNIT_SIZE;
                break;
        }
        // Wrap around the screen
        if (head.x < 0) head.x = WIDTH - UNIT_SIZE;
        else if (head.x >= WIDTH) head.x = 0;
        if (head.y < 0) head.y = HEIGHT - UNIT_SIZE;
        else if (head.y >= HEIGHT) head.y = 0;
        snake.add(0, head);
        snake.remove(snake.size() - 1);
    }
    private void checkFoodCollision()
    {
        if (snake.get(0).equals(food))
        {
            snake.add(new Point(-1, -1));  // Add a placeholder segment to be replaced in the next move
            spawnFood();
        }
    }
    private void checkSelfCollision()
    {
        Point head = snake.get(0);
        for (int i = 1; i < snake.size(); i++)
        {
            if (head.equals(snake.get(i)))
            {
                gameOver();
            }
        }
    }
    private void gameOver()
    {
        running = false;
        timer.stop();
        int option = JOptionPane.showOptionDialog(this, "Game Over! Would you like to play again?", "Snake Game",
                JOptionPane.YES_NO_OPTION, JOptionPane.INFORMATION_MESSAGE, null, null, JOptionPane.YES_OPTION);
        if (option == JOptionPane.YES_OPTION) {
            startGame();
        } 
        else
        {
            System.exit(0);
        }
    }
    @Override
    public void paint(Graphics g)
    {
        super.paint(g);
        // Draw background
        g.setColor(Color.BLACK);
        g.fillRect(0, 0, WIDTH, HEIGHT);
        // Draw food
        g.setColor(Color.RED);
        g.fillRect(food.x, food.y, UNIT_SIZE, UNIT_SIZE);
        // Draw snake
        for (Point point : snake)
        {
            g.setColor(Color.GREEN);
            g.fillRect(point.x, point.y, UNIT_SIZE, UNIT_SIZE);
            g.setColor(Color.BLACK);
            g.drawRect(point.x, point.y, UNIT_SIZE, UNIT_SIZE);
        }
    }
    public static void main(String[] args)
    {
        new SnakeGame();
    }
}
