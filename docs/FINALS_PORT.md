# 决赛基线

决赛以上位初赛 `c1425ef` 为基础。首件确认前只抓普通物资。确认后按核心、普通、伤员选物和分离，同类搜寻就近。沿用初赛的夹内漏框和归侧、分离次数、搜索换点、门口侧挤和三件重推。正式入口默认保存录像和日志，赛间预留 10 GB。

决赛按普通左右夹爪动作处理混装，禁用抓后自动抬爪滤除、橙黑直退滤除、门口横移滤除及分离抬爪 `U=8200`。首件确认已合入下位 `Final_task@6484448`。首次盲推前的 83° 补丁已通过离线检查，等待对端合入并烧录。[下位配套与接口](CROSS_REPO_REQUESTS.md)

决赛上位机位于 `/home/sunrise/RDK_X5/finals`。比赛流程和定位基线来自初赛 `302427138e426536673738d83cdf57ac6cd7242f`。当前模型使用 `vision/x5_output_640/hardcases_e24_x5_bayese_640x640_nv12.bin`，SHA-256 为 `bf632fd2af6f4d2bb8cb556b1e4fe6505f2a1837f4b97f0075402328af3b3c24`。六类顺序沿用正式类别表，置信阈值为 0.20，NMS 为 0.45。

桌面入口为「决赛-正式比赛」「决赛-物资测距标定」「决赛-识别区域绘制」。先退出当前比赛或相机工具，再打开另一入口。初赛开机待机入口继续按原方式启动。两套程序共用相机、T265、雷达、GPIO 和底盘 UART，一次运行一套。

决赛程序使用本仓库内的 ROI、抓前分区、扫障边界及 105°/120° 测距表。两份测距绘图布局位于 `vision/captures/range_calibration/layouts/`，正式的距离参数位于 `vision/config/approach_range.json`。决赛运行文件使用本仓库 `rescue_map/runtime/` 和决赛专用 `/dev/shm/rdk-rescue-finals-*`，操作 socket 使用 `@rescue-finals-operator-<UID>`。历史运行记录和录制数据按各自项目继续保存。

RDK 已部署与初赛正式入口一致的 `formal-unload-guard` 定位程序及两个原生库，见 `localization/build/formal-unload-guard/provenance.json`。本机依赖包括 `vision/native/` 下的 JPU/VSE 动态库、`build-250/librealsense/` 下的 RealSense 2.50 与固件，以及 `t265_trajectory/build/t265_boot`。这些设备构建产物单独部署。决赛源码与人工作业标定由本地独立 Git 仓库跟踪。

模型权重在 RDK 单独部署。新克隆需另行将决赛权重放到上文的模型路径。仓库保存类别表、测距和其他标定配置。

决赛物料尺寸变化后的实车测距、爪内计数、抓取和投送效果待验证。50 张样例的识别测试及相机测速见 RDK 下载目录 `finals-model-20261118-i8hoe56r/`。
