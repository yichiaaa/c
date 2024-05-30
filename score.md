# c# 學生成績資訊系統

## 👉介面介紹一

<img src="https://github.com/yichiaaa/c/raw/main/score1.png" alt="介面設計" weight="300px">

##### 讀檔:先在listBox設定好格式，當資料匯入時就會一同附上
```
 private void 讀檔ToolStripMenuItem_Click(object sender, EventArgs e)
 {
     StreamReader inputFile;
     if (openFileDialog1.ShowDialog() == DialogResult.OK)
     {
         inputFile = File.OpenText(openFileDialog1.FileName);
         listBox1.Items.Clear();
         id.Clear();
         name.Clear();
         chinese.Clear();
         math.Clear();
         english.Clear();
         total.Clear();
         average.Clear();
         listBox1.Items.Add("學號\t\t姓名\t國文\t英文\t數學\t總分\t平均");
         listBox1.Items.Add("================================================");
         while (!inputFile.EndOfStream)
         {
             string myid = inputFile.ReadLine();
             id.Add(myid);
             string myname = inputFile.ReadLine();
             name.Add(myname);
             int mychinese = int.Parse(inputFile.ReadLine());
             chinese.Add(mychinese);
             int mymath = int.Parse(inputFile.ReadLine());
             math.Add(mymath);
             int myenglish = int.Parse(inputFile.ReadLine());
             english.Add(myenglish);
             int mytotal = mychinese + mychinese + mymath;
             total.Add(mytotal);
             double myaverage = double.Parse(inputFile.ReadLine());
             average.Add(myaverage);
             listBox1.Items.Add(myid + "\t" + myname + "\t" + mychinese + "\t" + mymath + "\t" + myenglish + "\t" + mytotal + "\t" + myaverage.ToString("n2"));
         }
         inputFile.Close();
         MessageBox.Show("讀檔成功!");
     }
     else
     {
         MessageBox.Show("取消讀檔!");
     }
 }
```
##### 存檔:
```
  private void 存檔ToolStripMenuItem_Click(object sender, EventArgs e)
  {
    StreamWriter outputFile;
    if (saveFileDialog1.ShowDialog() == DialogResult.OK)
    {
        outputFile = File.CreateText(saveFileDialog1.FileName);
        for (int index = 0; index < id.Count; index++)
        {
            outputFile.WriteLine(id[index]);
            outputFile.WriteLine(name[index]);
            outputFile.WriteLine(chinese[index]);
            outputFile.WriteLine(math[index]);
            outputFile.WriteLine(english[index]);
            outputFile.WriteLine(total[index]);
            outputFile.WriteLine(average[index]);
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
## 👉介面介紹二

<img src="https://github.com/yichiaaa/c/raw/main/score2.png" alt="介面設計" weight="300px">


##### 平均:自行定義array_average的計算方法，再使用進平均下拉按鈕中
```
 private double array_average(List<int> score)
 {
     int total = 0;

     for (int index = 0; index < id.Count; index++)
     {
         total += score[index];
     }
     return (double)total / id.Count;
 }

 private void 平均ToolStripMenuItem_Click(object sender, EventArgs e)
 {
     MessageBox.Show("國文平均為" + array_average(chinese).ToString("n2") + "分" + "英文平均為" + array_average(english).ToString("n2") + "分" + "數學平均為" + array_average(math).ToString("n2") + "分" + array_average(total).ToString("n2") + "分");
 }

```
##### 最高分:自行定義array_highest、find_highest_student的執行方法，再使用進最高分下拉按鈕中
```
 private int array_highest(List<int> score)
{
    int highest = score[0];

    for (int index = 1; index < id.Count; index++)
    {
        if (score[index] > highest)
        {
            highest = score[index];
        }
    }
    return highest;
}

private void find_highest_student(int highest, List<int> score, string result)
{
    for (int index = 0; index < id.Count; index++)
    {
        if (score[index] == highest)
        {
            result += "\n學號:" + id[index] + "\n姓名:" + name[index];
        }
    }
    MessageBox.Show(result);
}
private void 最高分ToolStripMenuItem_Click(object sender, EventArgs e)
{
    int chi_hi = array_highest(chinese);
    find_highest_student(chi_hi, chinese, "國文最高分為" + chi_hi + "分");
    int eng_hi = array_highest(english);
    find_highest_student(eng_hi, english, "英文最高分為" + eng_hi + "分");
    int mat_hi = array_highest(math);
    find_highest_student(mat_hi, math, "數學最高分為" + mat_hi + "分");
    int tot_hi = array_highest(total);
    find_highest_student(tot_hi, total, "總分最高分為" + tot_hi + "分");
}

```
##### 最低分:自行定義array_lowest、find_lowest_student的執行方法，再使用進最低分下拉按鈕中
```
private int array_lowest(List<int> score)
{
    int lowest = score[0];

    for (int index = 1; index < id.Count; index++)
    {
        if (score[index] < lowest)
        {
            lowest = score[index];
        }
    }
    return lowest;
}

private void find_lowest_student(int lowest, List<int> score, string result)
{
    for (int index = 0; index < id.Count; index++)
    {
        if (score[index] == lowest)
        {
            result += "\n學號:" + id[index] + "\n姓名:" + name[index];
        }
    }
    MessageBox.Show(result);
}
private void 最低分ToolStripMenuItem_Click(object sender, EventArgs e)
{
    int chi_lo = array_lowest(chinese);
    find_lowest_student(chi_lo, chinese, "國文最低分為" + chi_lo + "分");
    int eng_lo = array_lowest(english);
    find_lowest_student(eng_lo, english, "英文最低分為" + eng_lo + "分");
    int mat_lo = array_lowest(math);
    find_lowest_student(mat_lo, math, "數學最低分為" + mat_lo + "分");
    int tot_lo = array_lowest(total);
    find_lowest_student(tot_lo, total, "總分最低分為" + tot_lo + "分");
}

```
##### 最低分:自行定義array_lowest、find_lowest_student的執行方法，再使用進最低分下拉按鈕中
```
private int array_lowest(List<int> score)
{
    int lowest = score[0];

    for (int index = 1; index < id.Count; index++)
    {
        if (score[index] < lowest)
        {
            lowest = score[index];
        }
    }
    return lowest;
}

private void find_lowest_student(int lowest, List<int> score, string result)
{
    for (int index = 0; index < id.Count; index++)
    {
        if (score[index] == lowest)
        {
            result += "\n學號:" + id[index] + "\n姓名:" + name[index];
        }
    }
    MessageBox.Show(result);
}
private void 最低分ToolStripMenuItem_Click(object sender, EventArgs e)
{
    int chi_lo = array_lowest(chinese);
    find_lowest_student(chi_lo, chinese, "國文最低分為" + chi_lo + "分");
    int eng_lo = array_lowest(english);
    find_lowest_student(eng_lo, english, "英文最低分為" + eng_lo + "分");
    int mat_lo = array_lowest(math);
    find_lowest_student(mat_lo, math, "數學最低分為" + mat_lo + "分");
    int tot_lo = array_lowest(total);
    find_lowest_student(tot_lo, total, "總分最低分為" + tot_lo + "分");
}

```

