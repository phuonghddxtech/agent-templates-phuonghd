# kiro-templates

Tập hợp các template `.kiro/steering` cho Kiro CLI, phân loại theo tech stack.

## Cấu trúc

```
kiro-templates/
├── laravel/
│   └── .kiro/steering/
│       ├── product.md     # Mô tả sản phẩm, module chính
│       ├── tech.md        # Tech stack, packages, commands
│       └── structure.md   # Cấu trúc thư mục, conventions
├── nextjs/                # (sắp có)
└── README.md
```

## Cách dùng

### Thủ công

```bash
cp -r laravel/.kiro /path/to/your-project/
```

### Dùng shell function (khuyến nghị)

Thêm vào `~/.zshrc` hoặc `~/.bashrc`:

```bash
kiro-init() {
  STACK="${1:-laravel}"
  git clone --depth=1 https://github.com/phuonghddxtech/kiro-templates.git /tmp/kiro-tpl 2>/dev/null
  cp -r /tmp/kiro-tpl/$STACK/.kiro .
  rm -rf /tmp/kiro-tpl
  echo "✓ Kiro $STACK template applied"
}
```

Sau đó chạy trong thư mục dự án:

```bash
kiro-init laravel
```

## Sau khi áp dụng

Chỉnh sửa `product.md` cho phù hợp với dự án mới. `tech.md` và `structure.md` thường chỉ cần thay đổi nhỏ nếu cùng stack.

## Đóng góp

Thêm stack mới bằng cách tạo thư mục mới với cấu trúc `.kiro/steering/` tương tự.
