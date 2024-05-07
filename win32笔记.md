# win32福利踩坑分享

## 关于项目的配置就很麻烦

<img src="https://img-blog.csdnimg.cn/20210528144125823.png" alt="编译错误" style="zoom:100%;" />

无法解析main是因为你当前项目设置的是console启动，而不是windows启动。他会去找你的cpp中有没有main函数，我们只有WinMain。

则需要右键解决方案资源管理器里的工程的名字，选择`属性properties`-》`链接器linker`-》`系统system`-》`子系统-subsystem`
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021052814432460.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3RpbWJleQ==,size_16,color_FFFFFF,t_70)

我们选择`windows`





## 关于有些报错，实验指导书上未必对

比如`DlgProc`函数要重载`<windows.h>`的DlgProc函数，实验指导书的返回值是`BOOL`，但是在新的`<windows.h>`中是`INT_PTR`返回值。报错信息长这样：`incompatible with ...`



## vs创建

## 进程创建

```c++
SHELLEXECUTEINFO app = {0};
app.fMask = SEE_MASK_NOCLOSEPROCESS;
app.cbSize = sizeof(SHELLEXECUTEINFO);
app.lpVerb = "open";
app.lpFile = "a.bat";
app.nShow=SW_SHOWDEFAULT;
ShellExecuteEx(&app);
WaitForSingleObject(app.hProcess, INFINITE);
CloseHandle(app.hProcess);
```







# `win32`不用`VS`桌面应用工具的快速入门

## 创建主窗口

死代码直接修改就好

```cpp

int WINAPI WinMain(HINSTANCE hInst, HINSTANCE hPrevInst, LPSTR args, int ncmdshow) {
    WNDCLASSW wc = {0};

    wc.hbrBackground = (HBRUSH) (COLOR_WINDOW);
    wc.hCursor = LoadCursor(NULL, IDC_ARROW);
    wc.hInstance = hInst;
    wc.lpszClassName = L"myWindowClass";
    wc.lpfnWndProc = WindowProcedure;

    if (!RegisterClassW(&wc)) {
        return -1;
    }
    CreateWindowW(L"myWindowClass", L"My Window", WS_OVERLAPPEDWINDOW | WS_VISIBLE, 100, 100, 500, 500, NULL, NULL,
                  NULL, NULL);
    MSG msg = {0};
    while (GetMessage(&msg, NULL, NULL, NULL)) {
        TranslateMessage(&msg);
        DispatchMessage(&msg);
    }
    return 0;
}
```

## 处理信息

像这样

```c++
LRESULT CALLBACK WindowProcedure(HWND hwnd, UINT msg, WPARAM wp, LPARAM lp) {
    switch (msg) {
        case WM_COMMAND:

            switch (wp) {
                    
            }

            break;
        case WM_CREATE:
            break;
        case WM_DESTROY:
            PostQuitMessage(0);
            break;
        default:
            return DefWindowProcW(hwnd, msg, wp, lp);
    }
    return 0;
}
```