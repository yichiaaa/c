# c# 學生成績資訊系統

## 介面介紹一
  
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
