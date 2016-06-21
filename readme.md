# SVGA-Format

## 序

* SVGA 是一种专有动画格式
* SVGA 的类似格式是 GIF / A-PNG / WebP

## 格式规范

* SVGA 文件以 .svga 作为后缀使用（该后缀不是ISO格式）
* SVGA 使用 ZIP 进行压缩、打包
* SVGA 解压后不允许拥有子目录
* SVGA 打包前、解压后的文件名不允许包含非标准文件名字符存在（不允许中文、日文等字符）

## 图像文件

* 位图文件要求格式为 PNG-8 或 PNG-24
* 位图文件建议使用 pngquant 进行压缩
* 位图文件以 .png 后缀命名

## 描述文件

* 描述文件格式为 JSON，文件为 movie.spec。

### JSON 结构

```js
{
    ver: "1.0.0",                                // SVGA 格式版本号
    movie: {
        viewBox: {
            width: 300.0,
            height: 300.0
        },                                       // 画布大小
        fps: 20,                                 // 动画每秒播放帖数，合法值是 [1, 2, 3, 5, 6, 10, 12, 15, 20, 30, 60] 中的任意一个。
        frames: 144                              // 动画总帖数                
    },
    images: {
        Key: "Path"                              // Key 是位图键名，Path 是位图文件名。
    },
    sprites: [
        {
            imageKey: "AwesomeSprite",           // 元件所对应的位图键名
            frames: [
                {
                    alpha: 1.0,                  // 元件透明度
                    layout: {
                        x: 0,
                        y: 0,
                        width: 100,
                        height: 100
                    },                           // 元件初始约束大小
                    transform: {
                        a: 0,
                        b: 0,
                        c: 0,
                        d: 0,
                        tx: 0,
                        ty: 0
                    }                            // 元件变化矩阵，3 * 3 矩阵中的具体含义，参照 CSS transform。
                }
            ]                                    // 元件在每一帖中的表现，对于某一帖中隐藏的元件，也需要使用一个对象进行占位。
        }
    ]                                            // 元件列表，在数组中索引值越大，代表层级越高。
}
```

### 类型参考
* "1.0.0" = String
* 1.0 = Double
* 1 = Int
* true = Boolean