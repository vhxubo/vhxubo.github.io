---
title: "OpenGL(Windows) 配置 - Visual Studio 2017 + GLFW + GLAD"
date: 2020-04-14T11:47:33+08:00
type: post
tags: ["OpenGL"]
categories: ["开发者手册"]
toc: true
---

3D 图形学课程需要使用到 OpenGL ，参考已有教程配置总是遇到很多问题，毕竟部分教程已经过时了。

因此，结合我遇到的问题，写下一个条理更加清晰的新版配置流程。

## 先决条件

- Visual Studio 2017
- 良好的网络环境

## 配置好的目录结构

```
- [项目名]
    - [项目名]
        - glad.c
    - opengl
        - include
            - glad
                - glad.h
            - GLFW
                - glfw3.h
                - glfw3native.h
            - KHR
                - khrplatform.h
        - lib
            -glfw3.lib
```

## Visual Studio 2017 配置

安装 Visual Studio 2017 时，勾选 C++ 桌面开发

新建一个空项目，在项目目录下新建一个 `opengl` 文件夹

<details>
<summary>查看当前目录结构</summary>
<pre><code>
- [项目名]
    - opengl
        - include
        - lib
</code></pre>
</details>

## GLFW

[官网下载](http://www.glfw.org/download.html)

根据自己的电脑系统位数，选择对应的 `64-bit Windows binaries` 或 `32-bit Windows binaries`

1. 打开下载好的压缩包
2. 将 `include` 放入 `[项目名]/opengl` 目录中
3. 打开 `lib-vc2017` 文件夹 (对应 Visual Studio 2017)，将 `glfw3.lib` 放入 `[项目名]/opengl/lib` 目录中

<details>
<summary>查看当前目录结构</summary>
<pre><code>
- [项目名]
    - opengl
        - include
            - GLFW
                - glfw3.h
                - glfw3native.h
        - lib
            - glfw3.lib
</code></pre>
</details>

## GLAD

[下载地址](http://glad.dav1d.de/)

下载配置如下所示：

1. Language: C/C++
2. Specification: OpenGL
3. API gl: Version 4.6
4. Profile: Core
5. Options： 勾选 Generate a loader
6. 点击 Generate 生成
7. 下载 `glad.zip`

![下载配置](glad-download.png)

8. 打开 `glad.zip`
9. 将 `include` 放入 `[项目名]/opengl` 目录中
10. 将 `src` 中的 `glad.c` 放入 `[项目名]/[项目名]` 目录中

<details>
<summary>查看当前目录结构</summary>
<pre><code>
- [项目名]
    - [项目名]
        - glad.c
    - opengl
        - include
            - glad
                - glad.h
            - GLFW
                - glfw3.h
                - glfw3native.h
            - KHR
                - khrplatform.h
        - lib
            -glfw3.lib
</code></pre>
</details>

至此，文件目录结构配置完成。

## 项目配置

- 项目 -> [项目名] 属性
- VC++ 目录 -> 常规 -> 包含目录 填入  `..\opengl\include`
- VC++ 目录 -> 常规 -> 库目录 填入  `..\opengl\lib`
- 链接器 -> 附加依赖项 填入
    ```
    opengl32.lib
    glfw3.lib
    ```
- 将 `glad.c` 加入到项目中

## 测试代码

在 `main.cpp` 中加入以下代码，运行之后会生成一个黑色窗口。

```C++
#include <glad/glad.h>
#include <GLFW/glfw3.h>
#include <iostream>
using namespace std;

void framebuffer_size_callback(GLFWwindow* window, int width, int height);

int main() {
    glfwInit();
    glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);
    glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);
    glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);

    GLFWwindow *window = glfwCreateWindow(800, 600, "LearnOpenGL", NULL, NULL);
    if (window == NULL) {
        cout << "Failed to create GLFW window" << endl;
        glfwTerminate();
        return -1;
    }
    glfwMakeContextCurrent(window);

    if (!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress)) {
        std::cout << "Failed to initialize GLAD" << std::endl;
        return -1;
    }

    glViewport(0, 0, 800, 600);

    glfwSetFramebufferSizeCallback(window, framebuffer_size_callback);

    while (!glfwWindowShouldClose(window)) {
        glfwSwapBuffers(window);
        glfwPollEvents();
    }

    glfwTerminate();
    return 0;
}

void framebuffer_size_callback(GLFWwindow* window, int width, int height) {
    glViewport(0, 0, width, height);
}
```

## 参考链接

[OpenGL 开发环境配置（Windows） - Visual Studio 2017 + GLFW + GLAD 详细图文教程](https://blog.csdn.net/sigmarising/article/details/80470054)
