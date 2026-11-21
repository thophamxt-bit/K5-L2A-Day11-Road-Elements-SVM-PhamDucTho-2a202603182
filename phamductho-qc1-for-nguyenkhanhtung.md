# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Nguyễn Khánh Tùng (`nguyenkhanhtung`)        Người kiểm (học viên): Phạm Đức Thọ (`phamductho`)  
Ngày: 2026-11-21                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `nguyenkhanhtung-front.zip`, `nguyenkhanhtung-fisheye.zip`, `nguyenkhanhtung-manifest.json` (`revision: 1`, SHA-256 khớp manifest, `contains_images: false`)  
Số ảnh kiểm: 6 (`A01`, `A02`, `A04`, `A07`, `B03`, `B04` — trong đó **`A01` không lỗi**) (+ 7 ảnh thêm ghi riêng: `A13`, `A15`, `A16`, `B09`, `B10`, `B11`, `B12` đã kiểm nhanh định dạng & đủ 4 tag)   Số nhãn đã kiểm (shape + tag): 64 (40 shape + 24 tag trên 6 ảnh mẫu)  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 6 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 13 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 13 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 13 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 13 | 2 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 16 | 2 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 6 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 11 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 11 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 15 | 0 | chính |
| QC1-12 file | lỗi file | 3 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-06 | A02 | `lane`, #5 (`L2`) | chính | Sai thuộc tính `style`: gán `solid` trong khi vạch `L2` trên ảnh `A02` là vạch trắng đứt (`dashed`). |
| 2 | QC1-06 | B03 | `lane`, #9 (`R1`) | chính | Sai thuộc tính `style`: gán `solid` trong khi vạch phân làn trên `B03` là vạch trắng đứt (`dashed`). |
| 3 | QC1-04 | B03 | `lane`, #9 (`R1`) | chính | Sai phạm vi / điểm bắt đầu: polyline bắt đầu từ giữa ảnh `p0=(782.6, 360.6)`, bỏ sót vệt sơn trắng đầu tiên sát cản sau xe ở góc dưới-phải. |
| 4 | QC1-07 | B03 | `crosswalk`, #4 | chính | Thừa nhãn: gán polygon `crosswalk` tại vùng góc dưới-phải quanh `(1177.9, 552.7)`–`(1057.8, 621.8)` nơi không có vạch người đi bộ qua đường. |
| 5 | QC1-07 | B04 | `crosswalk` (bỏ sót) | chính | Bỏ sót hoàn toàn polygon `crosswalk` cho vùng vạch ngựa vạn bản lớn cắt ngang mặt đường ngay phía sau cản xe. |

*(Ghi chú ảnh kiểm không lỗi: **`A01`** — đủ 4 tag đúng, đủ 4 vạch `L1/L2/R1/R2` đúng thuộc tính & chiều vẽ, đủ `drivable direct/alternative`, đủ biển `traffic_sign` `information`, 0 lỗi.)*

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A07 | `road_check lint` báo `QC1-02` (chưa có `L1`), nhưng bên trái làn xe trên `A07` là dải phân cách bê tông không có vạch sơn. Miễn `QC1-02` (tương tự `A05`, `A06`) có đúng không? | Đã tạm miễn `QC1-02` theo quy tắc không vẽ bịa vạch khi ảnh không có vạch sơn (không làm đổi quyết định `Rework`). |

## Quyết định
Lỗi nặng: 0   Lỗi chính: 5 / 64 nhãn = 7.81 %   Lỗi nhẹ: 0   Ca chờ lead: 0  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Không có lỗi nặng (cảnh báo `QC1-02` trên `A07` được miễn vì không có vạch sơn bên trái), nhưng tỉ lệ lỗi chính là **5 / 64 = 7,81 % > 5 %** số nhãn đã kiểm → theo luật Phiếu QC 1 phải **Rework** để sửa 5 lỗi chính nêu trên (đặc biệt là `style=dashed` ở `A02`/`B03`, nối đủ vạch gần xe ở `B03`, xoá `crosswalk` thừa ở `B03` và bổ sung `crosswalk` bị sót ở `B04`).

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
