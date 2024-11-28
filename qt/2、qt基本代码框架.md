```c++
#include <QApplication>

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);

    return app.exec();
}
```

### 使用.ui文件
#### 文件结构
![[Pasted image 20241111153336.png]]
#### 文件名字
如果.iu中`QWidget`的对象名字`Widget`，那么头文件的名字就是`Widget.h`，源文件的名字就是`Widget.cpp`

#### Widget.h
1. `Ui`命名空间中的`Widget`类会在`ui_widget.h`实现，将会继承`Ui_Widget`类
2. `Q_OBJECT`给moc使用
```
#pragma once

#include <QWidget>

namespace Ui {
class Widget;
}

class Widget : public QWidget {
    Q_OBJECT

  public:
    explicit Widget(QWidget *parent = 0);
    ~Widget();

  private:
    Ui::Widget *ui;
};
```

#### Widget.cpp
```
#include "widget.h"
#include "ui_widget.h"

Widget::Widget(QWidget *parent)
    : QWidget(parent), ui(new Ui::Widget) {
    ui->setupUi(this);
}

Widget::~Widget() {
    delete ui;
}

```
