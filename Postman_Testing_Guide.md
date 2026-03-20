# Hướng dẫn Kiểm thử Postman (Postman Testing Guide)

Dưới đây là các bước và dữ liệu mẫu (JSON) để bạn copy vào Postman và chụp ảnh minh chứng đưa vào file Word theo yêu cầu.

## 1. Tạo Product (Tự động tạo Inventory)
- **Method:** `POST`
- **URL:** `http://localhost:3000/api/v1/products`
- **Body (raw > JSON):**
```json
{
  "title": "Iphone 15 Pro Max",
  "price": 30000000,
  "description": "Điện thoại Apple mới nhất"
}
```
- **Kết quả:** Trả về thông tin Product vừa tạo (lưu ý copy cái `_id` của product để dùng cho các bước sau). Hệ thống sẽ tự động tạo một Inventory với `stock: 0, reserved: 0, soldCount: 0`.

## 2. Xem toàn bộ Inventory (Populate Product)
- **Method:** `GET`
- **URL:** `http://localhost:3000/api/v1/inventories`
- **Kết quả:** Trả về danh sách inventory, trong đó thông tin `product` sẽ được nhúng chi tiết bên trong.

## 3. Thêm Stock (Add_stock)
- **Method:** `POST`
- **URL:** `http://localhost:3000/api/v1/inventories/add-stock`
- **Body (raw > JSON):**
*(Thay `<Product_ID>` bằng `_id` lấy được ở bước 1)*
```json
{
  "product": "<Product_ID>",
  "quantity": 50
}
```
- **Kết quả:** `stock` tăng thêm 50.

## 4. Xóa Stock (Remove_stock)
- **Method:** `POST`
- **URL:** `http://localhost:3000/api/v1/inventories/remove-stock`
- **Body (raw > JSON):**
```json
{
  "product": "<Product_ID>",
  "quantity": 10
}
```
- **Kết quả:** `stock` giảm đi 10 (còn 40, nếu ở bước trên cộng 50).

## 5. Đặt hàng (Reservation)
- **Method:** `POST`
- **URL:** `http://localhost:3000/api/v1/inventories/reservation`
- **Body (raw > JSON):**
```json
{
  "product": "<Product_ID>",
  "quantity": 5
}
```
- **Kết quả:** `stock` giảm đi 5, `reserved` tăng lên 5.

## 6. Đã bán (Sold)
- **Method:** `POST`
- **URL:** `http://localhost:3000/api/v1/inventories/sold`
- **Body (raw > JSON):**
```json
{
  "product": "<Product_ID>",
  "quantity": 5
}
```
- **Kết quả:** `reserved` giảm đi 5, `soldCount` tăng lên 5.

--- 

*Lưu ý: Mở MongoDB Compass kiểm tra lại xem dữ liệu đã được lưu thành công chưa, chạy lệnh `npm start` hoặc `node ./bin/www` để start server trước khi test Postman.*
