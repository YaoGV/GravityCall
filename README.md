# Gravity Call

一个为现场而生的 Windows 桌面随机点名工具。深色控制台 + 右下角防误触圆形悬浮球，支持权重爆率、自动重置奖池、系统托盘常驻。

## 使用

1. 打开 `GravityCall.exe`。
2. 在「导入名单」中通过文本粘贴、Excel / CSV 或 Word 文档导入成员。
3. 在「概率调整」中为成员设置权重，爆率会实时归一化。
4. 单击右下角圆形悬浮球立即点名；长按 0.5 秒后可拖动悬浮球；右键悬浮球可打开菜单。
5. 关闭主面板不会退出程序：程序会缩到系统托盘，悬浮球继续待命。托盘右键 →「退出程序」会二次确认后退出。
6. 名单、权重和本轮抽奖池进度会自动保存，重启后从上次状态继续。
7. 结果弹窗打开时，直接继续点击悬浮球即可无限连抽，弹窗会即时刷新名字。

> 抽奖池中的成员被抽中后会移出，抽完一轮才会自动重置。

## 数据存储

名单、权重和本轮奖池进度通过用户级 `QSettings` 持久化（Windows 下位于 `HKEY_CURRENT_USER\Software\GravityCall\Gravity Call`），不会写入 PyInstaller 的临时解压目录。重启程序后会自动恢复。

## 操作细节

- 快速单击悬浮球：立即点名，结果秒出。
- 按住悬浮球超过 0.5 秒：进入拖拽模式，松开不会触发点名，避免误触。
- `Ctrl + D`：在主面板中快速点名。
- 名单默认覆盖导入；开启「追加模式」后会追加并去重。

## 开发运行

```powershell
pip install pyside6 pillow pyinstaller pandas openpyxl python-docx
python main.py
```

生成 256×256 引力波图标：

```powershell
python main.py --generate-icon
```

## 打包

```powershell
python -m PyInstaller --noconfirm --clean -F -w --name GravityCall `
  --icon=icon.ico `
  --add-data "qr_code.png;." `
  --add-data "icon.ico;." `
  --hidden-import=openpyxl `
  main.py
```

产物：`dist/GravityCall.exe`。

## 运行时资源

- `qr_code.png`：赞赏码，显示在「捐赠支持」页。
- `icon.ico`：由 `main.py --generate-icon` 使用 Pillow 自动绘制的 256×256 多尺寸图标。

## 致谢

开发者：s1rius_black8  
AI 辅助：DeepSeek  
特别鸣谢：古德赖可
