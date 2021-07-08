using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Pac_Man
{
    public partial class pacmanForm : Form
    {
        private bool goup, godown, goleft, goright, isGameOver;
        private int score, playerSpeed, redGhostSpeed, orangeGhostSpeed, pinkGhostX, pinkGhostY;
        
        
        
        public pacmanForm()
        {
            InitializeComponent();
            ResetGame();
        }

        private void keyisup(object sender, KeyEventArgs e)
        {
            if (e.KeyCode == Keys.Up)
            {
                goup = false;

            }
            if (e.KeyCode == Keys.Down)
            {
                godown = false;

            }
            if (e.KeyCode == Keys.Left)
            {
                goleft = false;

            }
            if (e.KeyCode == Keys.Right)
            {
                goright = false;

            }
        }

        private void keyisdown(object sender, KeyEventArgs e)
        {
            if (e.KeyCode == Keys.Up)
            {
                goup = true;
                
            }
            if (e.KeyCode == Keys.Down)
            {
                godown = true;

            }
            if (e.KeyCode == Keys.Left)
            {
                goleft = true;

            }
            if (e.KeyCode == Keys.Right)
            {
                goright = true;

            }

            if (e.KeyCode == Keys.Enter && isGameOver == true)
            {
                ResetGame();
            }

        }

        private void mainGameTimer(object sender, EventArgs e)
        {
            txtScore.Text = "Score: " + score;
            
            //pacman controls
            if (goleft == true)
            {
                pacman.Left -= playerSpeed;
                pacman.Image = Properties.Resources.left;
            }
            if (goright == true)
            {
                pacman.Left += playerSpeed;
                pacman.Image = Properties.Resources.right;
            }
            if (godown == true)
            {
                pacman.Top += playerSpeed;
                pacman.Image = Properties.Resources.down;
            }
            if (goup == true)
            {
                pacman.Top -= playerSpeed;
                pacman.Image = Properties.Resources.Up;
            }

            //if pacman goes through left/right wall
            if (pacman.Left < -10)
            {
                pacman.Left = 680;
            }

            if (pacman.Left > 680)
            {
                pacman.Left = -10;
            }


            if (pacman.Top < -10)
            {
                pacman.Top = 550;
            }

            if (pacman.Top > 550)
            {
                pacman.Left = -10;
            }
            foreach (Control x in this.Controls)
            {
                //intersect with a coin 
                if (x is PictureBox)
                {
                    if ((string) x.Tag == "coin" && x.Visible == true) 
                    {
                        if (pacman.Bounds.IntersectsWith(x.Bounds))
                        {
                            score++;
                            x.Visible = false;
                            

                        }
                    }
                }

                if ((string)x.Tag == "wall")
                {
                    if (pacman.Bounds.IntersectsWith(x.Bounds))
                    {
                        //end game
                        GameOver("You lose!");

                    }

                    if (pinkGhost.Bounds.IntersectsWith(x.Bounds))
                    {
                        pinkGhostX = -pinkGhostX;
                    }
                }
                if ((string)x.Tag == "ghost")
                {
                    if (pacman.Bounds.IntersectsWith(x.Bounds))
                    {
                        //end game
                        GameOver("You lose!");

                    }
                }
            }
            //Red ghost movement
            redGhost.Left += redGhostSpeed;
            if (redGhost.Bounds.IntersectsWith(pictureBox1.Bounds) ||
                redGhost.Bounds.IntersectsWith(pictureBox2.Bounds))
            {
                redGhostSpeed  = -redGhostSpeed;
            }

            //Orange ghost movement
            orangeGhost.Left -= orangeGhostSpeed;
            if (orangeGhost.Bounds.IntersectsWith(pictureBox4.Bounds) || orangeGhost.Bounds.IntersectsWith(pictureBox3.Bounds))
            {
                orangeGhostSpeed = -orangeGhostSpeed;
            }
            
            //Pink ghost movement
            pinkGhost.Left -= pinkGhostX;
            pinkGhost.Top -= pinkGhostY;
            if (pinkGhost.Top < 1 || pinkGhost.Top + pinkGhost.Height > ClientSize.Height - 2)
            {
                pinkGhostY = -pinkGhostX;
            }

            if (pinkGhost.Left < 0 || pinkGhost.Left > 490)
            {
                pinkGhostX = -pinkGhostX;
            }

            if (score == 42)
            {
                GameOver("You win!");
            }

        }

        private void ResetGame()
        {
            txtScore.Text = "Score: 0";
            score = 0;

            playerSpeed = 8;
            redGhostSpeed = 5;
            orangeGhostSpeed = 5;
            pinkGhostX = 5;
            pinkGhostY = 5;

            isGameOver = false;
            pacman.Left = 23;
            pacman.Top = 50;
            

            redGhost.Left = 217;
            redGhost.Top = 68;

            orangeGhost.Left = 280;
            orangeGhost.Top = 317;

            pinkGhost.Left = 440;
            pinkGhost.Top = 175 ;

            
            
            gameTimer.Start();


        }

        private void GameOver(string message)
        {
            isGameOver = true;
            gameTimer.Stop();
            txtScore.Text += Environment.NewLine + message;
        }
    }
}
