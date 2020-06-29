# 视频去背景方案调研


## 一. 机器学习方法（聚类）
1.  GMM（Gaussian mixture model）
    - 论文信息：[Zivkovic Z. Improved adaptive Gaussian mixture model for background subtraction[C]//Proceedings of the 17th International Conference on Pattern Recognition, 2004. ICPR 2004. IEEE, 2004, 2: 28-31.](https://ieeexplore.ieee.org/abstract/document/1333992/)
    - 开源实现
        1. >cv2.createBackgroundSubtractorMOG2()
        2. 一个简单开源实例   
           >[https://github.com/guichristmann/GMM-BgExtractor](https://github.com/guichristmann/GMM-BgExtractor)

    - 特点：受到图像序列的时序影响，当人物移动时，人物的移动轨迹容易在背景上留下ghost，消解速度较慢，处理一帧的时间大约在20ms内（320 * 240， 2GHz， 2004）
    - 评价：实现难度低，满足无绿幕去背景要求，但效果不理想。

2.  K-NN（K-Nearest Neigbours ）
    - 论文信息：[Zivkovic Z, Van Der Heijden F. Efficient adaptive density estimation per image pixel for the task of background subtraction[J]. Pattern recognition letters, 2006, 27(7): 773-780.](https://www.sciencedirect.com/science/article/abs/pii/S0167865505003521)
    - 开源实现
        1. >cv2.createBackgroundSubtractorKNN()
    - 特点：对前一种方法进行了改进，使得细节处理效果较好，并且对复杂画面（树与背景）的处理效果更好，对人像的效果有待对比。
    - 评价：实现难度低，满足无背景要求，在更复杂的场景下比方案1有一定的提升。
3.  ViBe
    - 论文信息：[Barnich O, Van Droogenbroeck M. ViBe: A universal background subtraction algorithm for video sequences[J]. IEEE Transactions on Image processing, 2010, 20(6): 1709-1724.](https://ieeexplore.ieee.org/abstract/document/5672785)
    - 开源实现
        >https://github.com/upcAutoLang/BackgroundSplit-OpenCV
    - 特点：只需要一帧图像即可完成初始化，采用随即替换更新样本值，计算量小，处理速度快，ghost消融速度快，应对噪声稳定
    - 评价：在运动物体检测及前景背景分离中表现良好，但对于主播拍摄场景下的主播与运动物体的判定效果不确定
    
4.  A method from Hao-Zhi Huang
    - 论文信息：[Huang H, Fang X, Ye Y, et al. Practical automatic background substitution for live video[J]. Computational Visual Media, 2017, 3(3): 273-284.](https://link.springer.com/article/10.1007/s41095-016-0074-0)
    - 开源实现 暂无
    - 特点：使用色线模型对北京切割的高斯混合模型进行了改进，使用Alpha遮罩细化分割边界，添加了自动前景颜色调整的步骤。性能：640*480， Intel 3.4 GHz Core i7-3770， 10fps（仅cpu），可以通过GPU并行化以实时帧速率运行。
    - 效果展示：[41095_2016_74_MOESM1_ESM.mp4](https://static-content.springer.com/esm/art%3A10.1007%2Fs41095-016-0074-0/MediaObjects/41095_2016_74_MOESM1_ESM.mp4)
    - 评价：满足我们的场景，并拥有相对可以接受的性能。性能瓶颈主要在alpha遮罩上，如果不使用alpha遮罩细化边框可以拥有更好的性能。

## 二. 深度学习方法（实时语义分割）
1.  ENet
    - 论文信息：[ENet: A Deep Neural Network Architecture for
Real-Time Semantic Segmentation](https://arxiv.org/pdf/1606.02147.pdf)
    - 开源实现
    1. >https://github.com/TimoSaemann/ENet  
    2. >https://github.com/kwotsin/TensorFlow-ENet
    - 特点：使用深度神经网络进行实时语义分割，是一个以在移动设备上运行为目标的网络，允许以更快，更高效的方式进行大规模计算。
    - 评价：用于复杂场景的语义分割，相对主播去背景场景来说过于复杂，gpu性能要求高，实用性有待测试。
    - 性能：
    <table>
    <tr>
        <td>NVIDIA TX1</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>NVIDIA Titan X</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>480×320</td>
        <td></td>
        <td> 640×360 </td>
        <td></td>
        <td> 1280×720</td>
        <td></td>
        <td> 640×360 </td>
        <td></td>
        <td> 1280×720</td>
        <td></td>
        <td>1920×1080</td>
        <td></td>
    </tr>
    <tr>
        <td>ms</td>
        <td>fps</td>
        <td>ms</td>
        <td>fps</td>
        <td>ms</td>
        <td>fps</td>
        <td>ms</td>
        <td>fps</td>
        <td>ms</td>
        <td>fps</td>
        <td>ms</td>
        <td>fps</td>
    </tr>
    <tr>
        <td>47</td>
        <td>21.1</td>
        <td>69</td>
        <td>14.6</td>
        <td>262</td>
        <td>3.8</td>
        <td>7</td>
        <td>135.4</td>
        <td>21</td>
        <td>46.8</td>
        <td>46</td>
        <td>21.6</td>
    </tr>
    <tr>
        <td></td>
    </tr>
    </table>
