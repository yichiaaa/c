# c# 學生成績資訊系統

## 👉介面介紹一

<img src="https://github.com/yichiaaa/c/raw/main/score1.png" alt="介面設計" >

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

<img src="https://github.com/yichiaaa/c/raw/main/score2.png" alt="介面設計" >


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
##### 排序:自行定義Swap的執行方法，再使用進最排序下拉按鈕中
```
 private void Swap(List<string> str, int a, int b)
 {
     string temp = str[a];
     str[a] = str[b];
     str[b] = temp;
 }

 private void Swap(List<int> num, int a, int b)
 {
     int temp = num[a];
     num[a] = num[b];
     num[b] = temp;
 }

 private void Swap(List<double> average, int a, int b)
 {
     double temp = average[a];
     average[a] = average[b];
     average[b] = temp;
 }
private void 排序ToolStripMenuItem_Click(object sender, EventArgs e)
{
    int maxIndex, maxValue;
    for (int startScan = 0; startScan < id.Count - 1; startScan++)
    {
        maxIndex = startScan;
        maxValue = total[startScan];
        for (int index = startScan + 1; index < id.Count; index++)
        {
            if (total[index] > maxValue)
            {
                maxValue = total[index];
                maxIndex = index;
            }
        }
        Swap(chinese, maxIndex, startScan);
        Swap(math, maxIndex, startScan);
        Swap(english, maxIndex, startScan);
        Swap(total, maxIndex, startScan);
        Swap(average, maxIndex, startScan);
        Swap(id, maxIndex, startScan);
        Swap(name, maxIndex, startScan);
    }
    listBox1.Items.Clear();
    listBox1.Items.Add("學號\\姓名\t國文\t英文\t數學\t總分\t平均");
    listBox1.Items.Add("========================================");
    for (int index = 0; index < id.Count; index++)
    {
        listBox1.Items.Add(id[index] + "\t" + name[index] + "\t" + chinese[index] + "\t" + english[index] + "\t" + math[index] + "\t" + total[index] + "\t" + average[index].ToString("n2"));
    }
}

```

## 👉介面介紹三

<img src="https://github.com/yichiaaa/c/raw/main/score3.png" alt="介面設計" >

##### 新增:
```
private void 新增ToolStripMenuItem_Click(object sender, EventArgs e)
{
    addfrm myaddfrm = new addfrm();
    myaddfrm.ShowDialog();
    if (!myaddfrm.cancel)
    {
        if (query(myaddfrm.id) == -1)
        {
            id.Add(myaddfrm.id);
            name.Add(myaddfrm.name);
            chinese.Add(myaddfrm.chi);
            english.Add(myaddfrm.eng);
            math.Add(myaddfrm.mat);
            int tot = myaddfrm.chi + myaddfrm.eng + myaddfrm.mat;
            total.Add(tot);
            double ave = tot / 3.0;
            average.Add(ave);
            listBox1.Items.Add(myaddfrm.id + "\t" + myaddfrm.name + "\t" + myaddfrm.chi + "\t" + myaddfrm.eng + "\t" + myaddfrm.mat + "\t" + tot + "\t" + ave.ToString("n2"));
            MessageBox.Show("學號" + myaddfrm.id + "資料新增成功!");
        }
        else
        {
            MessageBox.Show("學號" + myaddfrm.id + "已存在，無法新增!");
        }
    }
    else
    {
        MessageBox.Show("取消新增!");
    }
}
```
##### 並在另一個視窗中進行學號、姓名各項成績的資訊的填寫
<img src="https://github.com/yichiaaa/c/raw/main/add.png" alt="介面設計" >

```
private void button1_Click(object sender, EventArgs e)
{
    if (textBox1.Text != "")
    {
        qid = textBox1.Text;
        cancel = false;
        this.Close();
    }
    else
    {
        MessageBox.Show("請輸入欲刪除之學號!");
    }
}
```
##### 查詢:定義query的執行方法，再使用進最排序下拉按鈕中
```
private int query(string qid)
{
    bool found = false;
    int index = 0;
    int position = -1;

    while (!found && index < id.Count)
    {
        if (id[index] == qid)
        {
            found = true;
            position = index;
        }
        index++;
    }
    return position;
}

private void 查詢ToolStripMenuItem1_Click(object sender, EventArgs e)
{
    query queryfrm = new query();
    queryfrm.ShowDialog();
    if (!queryfrm.cancel)
    {
        int pos = query(queryfrm.qid);
        if (pos >= 0)
        {
            MessageBox.Show("學號:" + id[pos] + "\n姓名:" + name[pos] + "\n國文:" + chinese[pos] + "\n英文:" + english[pos] + "\n數學:" + math[pos] + "\n總分:" + total[pos] + "\n平均:" + average[pos].ToString("n2"));
        }
        else
        {
            MessageBox.Show("學號" + queryfrm.qid + "不存在!");
        }
    }
    else
    {
        MessageBox.Show("取消查詢");
    }
}
```
##### 並在另一個視窗中進行查詢學號的填寫
<img src="https://github.com/yichiaaa/c/raw/main/query.png" alt="介面設計" >

```
private void button1_Click(object sender, EventArgs e)
{
    if (textBox1.Text != "")
    {
        qid = textBox1.Text;
        cancel = false;
        this.Close();
    }
    else
    {
        MessageBox.Show("請輸入欲查詢之學號!");
    }
}

private void button2_Click(object sender, EventArgs e)
{
    this.Close();
}

```

##### 刪除
```
    private void 刪除ToolStripMenuItem_Click(object sender, EventArgs e)
    {
        delfrm mydelfrm = new delfrm();
        mydelfrm.ShowDialog();
        if (!mydelfrm.cancel)
        {
            int pos = query(mydelfrm.qid);
            if (pos >= 0)
            {
                id.RemoveAt(pos);
                name.RemoveAt(pos);
                chinese.RemoveAt(pos);
                english.RemoveAt(pos);
                math.RemoveAt(pos);
                total.RemoveAt(pos);
                average.RemoveAt(pos);
                listBox1.Items.RemoveAt(pos + 2);
                MessageBox.Show("學號:" + mydelfrm + "已被刪除!");
            }
            else
            {
                MessageBox.Show("學號" + mydelfrm.qid + "不存在!");
            }
        }
        else
        {
            MessageBox.Show("取消刪除");
        }
    }
}
```
##### 並在另一個視窗中進行學號的填寫並刪除
<img src="https://github.com/yichiaaa/c/raw/main/delete.png" alt="介面設計" >

```
private void button1_Click(object sender, EventArgs e)
{
    if (textBox1.Text != "")
    {
        qid = textBox1.Text;
        cancel = false;
        this.Close();
    }
    else
    {
        MessageBox.Show("請輸入欲刪除之學號!");
    }
}
```

## 👉相似程式延伸

##### 延伸使用至記帳程式
<img src="https://github.com/yichiaaa/c/raw/main/record.png" alt="介面設計" >
