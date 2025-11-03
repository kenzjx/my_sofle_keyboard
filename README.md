# My Sofle Keyboard - ZMK Firmware Configuration

Dự án cấu hình firmware ZMK (Zephyr-based Keyboard Firmware) cho bàn phím Sofle, một bàn phím split ergonomic với 58 phím.

## 📋 Mô Tả

Đây là repository chứa cấu hình firmware ZMK cho bàn phím Sofle với các tính năng:
- **Bàn phím split**: Hai nửa độc lập (trái/phải) sử dụng Nice!Nano v2
- **OLED Display**: Màn hình hiển thị thông tin trạng thái
- **Rotary Encoders**: Hai encoder cho điều khiển âm lượng và các chức năng khác
- **RGB Underglow**: Đèn LED RGB phía dưới bàn phím
- **Bluetooth**: Hỗ trợ kết nối không dây qua Bluetooth
- **Multiple Layers**: Hệ thống lớp phím với 4 layers (Base, Lower, Raise, Adjust)

## 🎯 Tính Năng

### Layers (Lớp phím)

1. **Base Layer (Mặc định)**: Layout QWERTY chuẩn
2. **Lower Layer**: Chứa các phím F1-F12, ký tự đặc biệt, và dấu
3. **Raise Layer**: Điều khiển Bluetooth, phím điều hướng, và các phím chức năng
4. **Adjust Layer**: Cài đặt RGB, điều khiển nguồn, và quản lý Bluetooth

### Controls

- **Rotary Encoders**: Điều chỉnh âm lượng khi xoay, nhấn để chuyển layer
- **Bluetooth**: Hỗ trợ kết nối tới 5 thiết bị khác nhau
- **RGB Controls**: Điều chỉnh màu sắc, độ sáng, và hiệu ứng LED
- **External Power**: Điều khiển nguồn ngoài cho các thiết bị USB

## 🛠️ Cài Đặt và Build

### Yêu Cầu

- [ZMK Firmware](https://zmk.dev/)
- [West Tool](https://docs.zephyrproject.org/latest/develop/west/index.html)
- Python 3.x

### Các Bước Build

1. Clone repository này:
```bash
git clone git@github.com:kenzjx/my_sofle_keyboard.git
cd my_sofle_keyboard
```

2. Khởi tạo ZMK và dependencies:
```bash
west init -l config
west update
```

3. Build firmware:
```bash
west build -s zmk/app -b nice_nano_v2 -- -DSHIELD=sofle_left -DKEYMAP_CONFIG=sofle.keymap -DCONFIG_FILE=sofle.conf
west build -s zmk/app -b nice_nano_v2 -- -DSHIELD=sofle_right -DKEYMAP_CONFIG=sofle.keymap -DCONFIG_FILE=sofle.conf
```

Firmware đã build sẽ được lưu tại `build/zephyr/zmk.uf2`

## 📁 Cấu Trúc Dự Án

```
my_sofle_keyboard/
├── config/
│   ├── sofle.keymap      # Bản đồ phím (keymap)
│   ├── sofle.conf        # Cấu hình ZMK (OLED, encoders, RGB)
│   └── west.yml          # West manifest
├── boards/
│   └── shields/          # Shield definitions (nếu có)
├── zephyr/
│   └── module.yml        # Zephyr module config
├── build.yaml            # GitHub Actions build matrix
└── .github/
    └── workflows/
        └── build.yml     # CI/CD workflow
```

## 🔧 Tùy Chỉnh

### Thay Đổi Keymap

Chỉnh sửa file `config/sofle.keymap` để thay đổi layout phím. File này sử dụng Device Tree Syntax của ZMK.

### Cấu Hình Tính Năng

Chỉnh sửa file `config/sofle.conf` để bật/tắt các tính năng:
- `CONFIG_ZMK_DISPLAY=y`: Bật OLED display
- `CONFIG_EC11=y`: Bật rotary encoders
- `CONFIG_ZMK_RGB_UNDERGLOW=y`: Bật RGB underglow

## 📦 Flash Firmware

1. Đưa Nice!Nano vào chế độ bootloader (double-tap nút reset)
2. Copy file `zmk.uf2` vào ổ USB xuất hiện
3. Lặp lại cho nửa còn lại

## 🔗 Tài Liệu Tham Khảo

- [ZMK Documentation](https://zmk.dev/docs)
- [Sofle Keyboard](https://github.com/josefadamcik/SofleKeyboard)
- [Nice!Nano](https://nicekeyboards.com/nice-nano)

## 📝 License

MIT License - Xem file LICENSE để biết thêm chi tiết.

## 👤 Tác Giả

[kenzjx](https://github.com/kenzjx)

