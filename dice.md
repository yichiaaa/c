# c# Dice Game

## 👉骰寶遊戲介面設計
<img src="https://github.com/yichiaaa/c/raw/main/dice.png" alt="介面設計" weight="300px">

## 程式碼說明
  
```
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        int original, rest;

        private void Form1_Load(object sender, EventArgs e)
        {
            MessageBox.Show("歡迎光臨教學賭場\n十賭九輸請勿沉迷!");
            button2.Enabled = false;
            button3.Enabled = false;
            button4.Enabled = false;
            textBox1.Enabled = false;
            radioButton1.Checked = true;
        }
```
先進行剛進入介面的設定，在還沒「讀檔」前無法進行其他功能的使用
```
        private void button1_Click(object sender, EventArgs e)
        {
            StreamReader inputFile;

            if (openFileDialog1.ShowDialog() == DialogResult.OK)
            {
                inputFile = File.OpenText(openFileDialog1.FileName);
                listBox1.Items.Clear();
                while(!inputFile.EndOfStream)
                {
                    listBox1.Items.Add(inputFile.ReadLine());
                }
                inputFile.Close();
                MessageBox.Show("讀檔成功!");
                button2.Enabled = true;
                button3.Enabled = true;
                button4.Enabled = true;
                textBox1.Text = listBox1.Items[0].ToString();
                original = int.Parse(textBox1.Text);
                listBox1.Items.Add("上線日期" + DateTime.Now);
            }
            else
            {
                MessageBox.Show("取消讀檔!");
            }
        }
    }
}
```
利用openFileDialog1進行讀檔，可以讀取.txt檔設定初始進入賭場的本金

```
        private void button2_Click(object sender, EventArgs e)
        {
            StreamWriter outputFile;

            if (saveFileDialog1.ShowDialog()==DialogResult.OK)
            {
                outputFile = File.CreateText(saveFileDialog1.FileName);
                for(int i = 0; i < listBox1.Items.Count;i++)
                {
                    outputFile.WriteLine(listBox1.Items[i]);
                }
                outputFile.Close();
                MessageBox.Show("存檔成功!");
            }
            else
            {
                MessageBox.Show("取消存檔!");
            }
        }
```
存檔按鈕的設定，使用工具箱中「saveFileDialog1」的工具進行存檔
```
        private void button3_Click(object sender, EventArgs e)
        {
            if(listBox1.SelectedIndex >0)
            {
                listBox1.Items.RemoveAt(listBox1.SelectedIndex);
                MessageBox.Show("刪除成功!");
            }
            else
            {
                MessageBox.Show("您沒有選取任何資料!");
            }
        }
```
設定刪除的按鈕，也藉由判斷式進行除錯
```
        private void button4_Click(object sender, EventArgs e)
        {
            try
            {
                Random rand = new Random();
                rest = int.Parse(textBox1.Text);
                int bet = int.Parse(textBox2.Text);
                if(bet <= rest)
                {
                    int dice1 = rand.Next(6) + 1;
                    int dice2 = rand.Next(6) + 1;
                    int dice3 = rand.Next(6) + 1;
                    switch(dice1)
                    {
                        case 1:
                            pictureBox1.Image = Properties.Resources._1;
                            break;
                        case 2:
                            pictureBox1.Image = Properties.Resources._2;
                            break;
                        case 3:
                            pictureBox1.Image = Properties.Resources._3;
                            break;
                        case 4:
                            pictureBox1.Image = Properties.Resources._4;
                            break;
                        case 5:
                            pictureBox1.Image = Properties.Resources._5;
                            break;
                        case 6:
                            pictureBox1.Image = Properties.Resources._6;
                            break;
                    }
                    switch (dice2)
                    {
                        case 1:
                            pictureBox2.Image = Properties.Resources._1;
                            break;
                        case 2:
                            pictureBox2.Image = Properties.Resources._2;
                            break;
                        case 3:
                            pictureBox2.Image = Properties.Resources._3;
                            break;
                        case 4:
                            pictureBox2.Image = Properties.Resources._4;
                            break;
                        case 5:
                            pictureBox2.Image = Properties.Resources._5;
                            break;
                        case 6:
                            pictureBox2.Image = Properties.Resources._6;
                            break;
                    }
                    switch (dice3)
                    {
                        case 1:
                            pictureBox3.Image = Properties.Resources._1;
                            break;
                        case 2:
                            pictureBox3.Image = Properties.Resources._2;
                            break;
                        case 3:
                            pictureBox3.Image = Properties.Resources._3;
                            break;
                        case 4:
                            pictureBox3.Image = Properties.Resources._4;
                            
```
利用Random，讓pictureBox中的Resource隨機跑出骰子照片
```
        private void button5_Click(object sender, EventArgs e)
        {
            int result = rest - original;
            if(result>0)
            {
                MessageBox.Show("恭喜您贏了" + result.ToString("c") + "，謝謝光臨!");
            }
            if (result < 0)
            {
                result = -result;
                MessageBox.Show("抱歉您輸了" + result.ToString("c") + "，謝謝光臨!");
            }
            if (result == 0)
            {
                MessageBox.Show("您不賺也不賠，謝謝光臨!");
            }
            this.Close();
        }
```
定義結束按鈕，並計算剛一連串賭博遊戲中的勝負和輸贏金額
