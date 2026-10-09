# Gửi QR đăng nhập Zalo qua bot Telegram OpenClaw

Skill `openclaw-telegram-zalo-qr-delivery` hướng dẫn OpenClaw tự tạo QR đăng nhập Zalo Personal và gửi ảnh trực tiếp vào Telegram riêng của owner. Người dùng chỉ cần quét và xác nhận trên điện thoại, thay vì phải mở dashboard để nhập `connect zalouser`.

## Nội dung

- `openclaw-telegram-zalo-qr-delivery/SKILL.md`: skill hoàn chỉnh, có quy trình chọn đúng bot, agent, Telegram account, Zalo account và runtime.
- Gửi ảnh ngay khi QR xuất hiện, giữ tiến trình login chờ quét, kiểm tra biên nhận gửi và xác minh riêng trạng thái đăng nhập.
- Không tự cấp quyền, xóa lock đang chạy hoặc công khai QR lên web.

## Cài vào runtime cần sử dụng

Clone repo này, rồi sao chép **cả thư mục** `openclaw-telegram-zalo-qr-delivery` vào một thư mục skill được OpenClaw runtime đích đọc:

- Managed skills: `$OPENCLAW_STATE_DIR/skills`, hoặc `~/.openclaw/skills` nếu dùng state directory mặc định.
- Workspace skills: `<workspace-của-agent>/skills`, đặc biệt khi agent chỉ được đọc trong workspace.

Với Docker/member, cài bên trong đúng container/runtime; cài trên host không tự đồng bộ sang mọi member. Không sao chép config, token hoặc credential từ runtime khác.

Trên phiên bản CLI có hỗ trợ, kiểm tra:

```bash
openclaw skills --agent <agent-id> info openclaw-telegram-zalo-qr-delivery
```

Kiểm tra `--help` nếu CLI phiên bản khác. Skill cần được runtime nhận diện và cho phép model sử dụng.

## Sử dụng

Nhắn bot Telegram đã được cài skill:

> Gửi anh QR đăng nhập Zalo. Dùng skill openclaw-telegram-zalo-qr-delivery.

Bot cần quyền thực thi login và gửi media, plugin `zalouser` hoạt động, cùng DM Telegram của owner có thể nhận ảnh. Đây là **skill hướng dẫn**, không phải daemon hoặc plugin tự cấp quyền: gửi link GitHub cho bot không đồng nghĩa skill đã được cài hay vượt được policy hiện có.

## Kiểm thử và giới hạn

Skill đã qua kiểm tra frontmatter và được OpenClaw host nhận ở trạng thái `Ready`. Chưa kiểm thử gửi QR/đăng nhập thực tế end-to-end hoặc triển khai cho mọi member. QR là dữ liệu xác thực; chỉ gửi riêng cho owner đã xác minh và không commit QR, token hay credential vào repo.
