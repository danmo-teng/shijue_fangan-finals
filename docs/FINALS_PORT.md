# 决赛基线

决赛 main 已配对 `Final_Run/Final_task@4656c77`。首件正式投送为单普通，确认进区并完成本次退出后登记；首件后纯普通、核心 1～3 件整批直送，伤员单件。分离复用左右夹爪及真实整爪复审，每批最多三次。沿用送达确认与未确认超时退出。32 项相关离线检查通过，板端实际版本及实车效果待验。[本轮实现和接口边界](FINALS_QUESTIONNAIRE_SEPARATION_20261119.md)

上位已停用橙黑分离 `U=8200`、门口横移滤除和首件撞堆。下位 `FinalRun` 预设关闭抓后自动抬爪滤除。决赛现场需使用匹配固件。

决赛上位机位于 `/home/sunrise/RDK_X5/finals`。比赛流程和定位基线来自初赛 `302427138e426536673738d83cdf57ac6cd7242f`。当前模型使用 `yolo26n/x5_output_640_1119_final/yolo26n_6cls_640_1119_final_bpu_bayese_640x640_nv12.bin`，SHA-256 为 `e1cd7f3b54e14bbe48e3ab3119d64a34047fda2984024d26e2be475b10aeb12a`。六类顺序沿用正式类别表，置信阈值为 0.20，NMS 为 0.45。

桌面入口为「决赛-正式比赛」「决赛-物资测距标定」「决赛-识别区域绘制」。先退出当前比赛或相机工具，再打开另一入口。初赛开机待机入口继续按原方式启动。两套程序共用相机、T265、雷达、GPIO 和底盘 UART，一次运行一套。

决赛程序使用本仓库内的 ROI、抓前分区、扫障边界及 105°/120° 测距表。两份测距绘图布局位于 `vision/captures/range_calibration/layouts/`，正式的距离参数位于 `vision/config/approach_range.json`。决赛运行文件使用本仓库 `rescue_map/runtime/` 和决赛专用 `/dev/shm/rdk-rescue-finals-*`，操作 socket 使用 `@rescue-finals-operator-<UID>`。历史运行记录和录制数据按各自项目继续保存。

RDK 已部署与基线匹配的定位程序及两个原生库，见 `localization/build/formal-contact-wheel/provenance.json`。本机依赖包括 `vision/native/` 下的 JPU/VSE 动态库、`build-250/librealsense/` 下的 RealSense 2.50 与固件，以及 `t265_trajectory/build/t265_boot`。这些设备构建产物单独部署。决赛源码与人工作业标定由本地独立 Git 仓库跟踪。

模型权重在 RDK 单独部署。新克隆需另行将决赛权重放到上文的模型路径。仓库保存类别表、测距和其他标定配置。

决赛物料尺寸变化后的实车测距、爪内计数、抓取和投送效果待验证。50 张样例的识别测试及相机测速见 RDK 下载目录 `finals-model-20261118-i8hoe56r/`。
