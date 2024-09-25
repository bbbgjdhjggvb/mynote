![[Pasted image 20240515205425.png]]
#### Frame类
1. `Frame frame=new Frame("标题，如果没有参数就是无题目")`
2. `frame.setBounds(x,y,weight,height)`
3. `frame.setVisable(true)`
4. `fame.setLayout()`
	1. 顺序布局
	2. 东南西北中
	3. 表格布局
框架
```

public class JFrame extends Frame{
   public JFrame(){
        super();//没有标题
        setBounds(0,0,400,400);//设置大小和位置
        setVisible(true);//可见
        addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e){
                //发送exit信息

                //退出程序
                System.exit(0);
            } 
        });
   } 
   public static void main(String[] args) {
        JFrame frame=new JFrame(); 
   }
}
```
#### Panel类
1. 无法单独显示，必须在容器内
2. 方法和frame差不多

