File类指向文件或者文件夹
#### 目录列表
```
File path=new File(".");
String[] list=path.list();
if(list==null){
	
}
else{
	如果是文件夹会输出文件夹的名字，文件就输出文件的名字
}
```
##### 目录名字过滤器
1. 实现FilenameFilter接口，重写accept函数
2. 回调当作list的参数
```
class DirFilter implements FilenameFilter{
  String name;
  DirFilter(String name){
    this.name=name;
  }
  public boolean accept(File dir,String name){
    return name.contains("java");
  }
}
```
list方法会为每一个文件名字调用accept函数，path传入dir，文件或者文件夹名字传入name。

#### 目录过滤并且保存在File数组中
1. 调用File的成员函数listFiles()
2. 可实现FilenameFilter接口
3. 只能进入一级
4. 如果需要`List<File>`，则`List<File> filelist=Arrays.asList(files);`
```
  public static File[]local(File dir,String name){
    return dir.listFiles();
  }
```
5. 通过递归调用来保存文件
```
public class DirTreeInfo {
    public DirTreeInfo info;

    private List<File> files; 
    private List<File> dirs;
    private File path;

    public DirTreeInfo(File path){
        this.path=path;
        File[] tempfiles=path.listFiles();
        this.dirs=Arrays.asList(tempfiles);
        this.files=new ArrayList<>();
    }

    private void addfiles(DirTreeInfo other){
        this.files.addAll(other.files);
    }
    private DirTreeInfo recurseTree(File path){
        DirTreeInfo dti=new DirTreeInfo(path);
        for(File f:dti.dirs){
            if(f.isDirectory()){
                dti.addfiles(recurseTree(f));
            }
            else{
                dti.files.add(f);
            }
        }
        return dti;
    }
    public List<File> listFiles(){
        this.info=this.recurseTree(this.path);
        return this.info.files;
    }
}
```
6. FIle的isDirectory方法
7. File的ListFiles方法