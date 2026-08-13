## Task Information

- Task ID:
- Feature/Fix:
- Related Issue:

---

## A. Merge Request Convention

- [ ] Branch đúng naming convention.
- [ ] Chỉ chứa thay đổi của task hiện tại.
- [ ] Đã pull latest main.
- [ ] Đã self-review.
- [ ] Đã hoàn thành toàn bộ yêu cầu task.

---

## B. Clean Code

- [ ] Tuân thủ SRP.
- [ ] Không duplicate code.
- [ ] Không còn dead code.
- [ ] Không hard-code giá trị cấu hình.
- [ ] Naming rõ ràng và nhất quán.
- [ ] Không để lại TODO/FIXME tạm thời.

---

## C. C++ Review

- [ ] Forward declaration hợp lý.
- [ ] Không circular dependency.
- [ ] Không memory leak.
- [ ] Null check đầy đủ.
- [ ] Logging đúng chuẩn.
- [ ] Error handling đầy đủ.

---

## D. Blueprint Review

- [ ] Blueprint graph sạch và dễ đọc.
- [ ] Logic được tách Function/Macro hợp lý.
- [ ] Không còn node thừa.
- [ ] Không Blueprint Warning.
- [ ] Không lạm dụng Tick.
- [ ] Hạn chế Cast không cần thiết.

---

## E. Performance

- [ ] Không có logic nặng trong Tick.
- [ ] Không Get All Actors Of Class trong Tick.
- [ ] Không load asset đồng bộ không cần thiết.
- [ ] Đã xem xét tối ưu hóa.

---

## F. Multiplayer (Nếu áp dụng)

- [ ] Authority đúng.
- [ ] RPC đúng mục đích.
- [ ] Replication hợp lý.
- [ ] Đã test multiplayer flow.

---

## Reviewer Checklist

- [ ] Coding convention đạt yêu cầu.
- [ ] Blueprint convention đạt yêu cầu.
- [ ] Không phát hiện issue nghiêm trọng.
- [ ] Approve for merge.

---

## Review Comments

- Comment 1 lần cho cùng một loại lỗi.
- Comment "." nghĩa là lỗi tương tự đã được đề cập ở vị trí khác.
- Tác giả có trách nhiệm rà soát và sửa toàn bộ các vị trí tương tự.
