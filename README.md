# Calculator
This is a task from L2+ course

We used dump file in order to find the issue.

![image](https://github.com/wladengine/m04-optimization-Calculator/assets/7301775/077f5141-8a87-4d60-bef8-f0411f6f3a2c)
By clicking on 'Debug with Managed only' or 'Debug with mixed' we discovered the MainWindow.cs file with breaking place in code.

![image](https://github.com/wladengine/m04-optimization-Calculator/assets/7301775/4a28f68c-23fe-4881-a636-e79147856e0f)
We can see the root cause (non-convertable part of string) and can suggest fixes: either control input value in Button_Click_1() or special "input string fixing function".
I would prefer first one: it could be more testable:

```
private void Button_Click_1(object sender, RoutedEventArgs e)
{
      Button button = (Button)sender;
      // tb.Text += button.Content.ToString();
      tb.Text = AppendNewSymbol(tb.Text, button.Content.ToString());
}

internal string AppendNewSymbol(string inputString, string symbol)
{
    // here we perform any specific checks i.e. return of double-typed operation signs
}
```
