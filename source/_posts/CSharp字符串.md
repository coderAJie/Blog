---
title: C#字符串
categories: [C#]
---

##### 连接

- Join

  ```
  	string[] sarray = { "Hello", "From", "Tutorials", "Point" };
  	string message = String.Join("-", sarray);
  ```

- Concat

  ```
      string s1 = "00wqw12";
      string s2 = "0012";
      s1 = string.Concat(s1, s2);
  ```

- StringBuilder

  ```
      string s1 = "00wqw12";
      string s2 = "0012";
      StringBuilder sb = new StringBuilder();
      sb.Append(s1);
      sb.Append(s2);
      Debug.LogError(sb.ToString());   
  ```

##### 比较

- Equals相等

  ```
      string s1 = "00wqw12";
      string s2 = "0012";
      bool b = string.Equals(s1, s2);
  ```

- 为空

  ```
      string s1 = "00wqw12";
      bool b = string.IsNullOrEmpty(s1);
      bool b = string.IsNullOrWhiteSpace(s1);
  ```

- Compare不相同字符

  ```
      string s1 = "0000wqw12";
      string s2 = "0000wa";
      int c = string.Compare(s1, s2);
      //挨个比较字符Unicode值，大于为1，小于为-1，等于为0
  ```

- Contains包含

  ```
      string s1 = "0000wqw12";
      string s2 = "0000wqw121";
      bool b = s2.Contains(s1);
  ```

##### 修改

- Insert插入

  ```
      string s1 = "0000wqw12";
      s1 = s1.Insert(0, "ww");
  ```

- Remove删除

  ```
      string s1 = "0000wqw12";
      s1 = s1.Remove(1);
      s1 = s1.Remove(1,2);
  ```

- Replace替换

  ```
      string s1 = "0000wqw12";
      s1 = s1.Replace('0', '_');
      s1 = s1.Replace("0", "_");
  ```

- Substring截取

  ```
      string s1 = "0000wqw12";
      s1 = s1.Substring(2, 3);
  ```

- Split分割

- PadLeft填充

##### 查找

- IndexOf

  ```
      string s1 = "0000wqw12";
      index = s1.IndexOf('0');
      index = s1.IndexOf("00");
      index = s1.LastIndexOf("00");
  ```

##### Format

- C货币

  ```
  string.Format("{0:C}",0.2) 结果为：￥0.20 （英文操作系统结果：$0.20）
  string.Format("{0:C1}",23.15) 结果为：￥23.2 （保留一位小数）
  string.Format("市场价：{0:C}，优惠价{1:C}",23.15,19.82)
  ```

- D十进制

  ```
  string.Format("{0:D3}",23) 结果为：023
  string.Format("{0:D2}",1223) 结果为：1223，（精度说明符指示结果字符串中所需的最少数字个数。）
  ```

- E科学计数法

  ```
  Console.Write("{0:E}", 250000);   //2.500000E+005
  ```

- F固定点

  ```
  Console.Write("{0:F2}", 25);   //25.00
  Console.Write("{0:F0}", 25);   //25
  ```

- N逗号隔开数字

  ```
  string.Format("{0:N}", 14200) 结果为：14,200.00 （默认为小数点后面两位）
  string.Format("{0:N3}", 14200.2458) 结果为：14,200.246 （自动四舍五入）
  ```

- X十六进制

  ```
  Console.Write("{0:X}", 250);   //FA
  ```

- P百分比

  ```
  string.Format("{0:P}", 0.24583) 结果为：24.58% （默认保留百分的两位小数）
  string.Format("{0:P1}", 0.24583) 结果为：24.6% （自动四舍五入）
  ```

- 0占位符

  ```
  string.Format("{0:0000.00}", 12394.039) 结果为：12394.04
  string.Format("{0:0000.00}", 194.039) 结果为：0194.04
  string.Format("{0:###.##}", 12394.039) 结果为：12394.04
  string.Format("{0:####.#}", 194.039) 结果为：194
  ```

- 日期

  ```
  string.Format("{0:d}",System.DateTime.Now) 结果为：2009-3-20 （月份位置不是03）
  string.Format("{0:D}",System.DateTime.Now) 结果为：2009年3月20日
  string.Format("{0:f}",System.DateTime.Now) 结果为：2009年3月20日 15:37
  string.Format("{0:F}",System.DateTime.Now) 结果为：2009年3月20日 15:37:52
  string.Format("{0:g}",System.DateTime.Now) 结果为：2009-3-20 15:38
  string.Format("{0:G}",System.DateTime.Now) 结果为：2009-3-20 15:39:27
  string.Format("{0:m}",System.DateTime.Now) 结果为：3月20日
  string.Format("{0:t}",System.DateTime.Now) 结果为：15:41
  string.Format("{0:T}",System.DateTime.Now) 结果为：15:41:50
  ```

  
