---
title: "Đồ thị Con Đường Truy Xuất Tour"
author: "Bạn"
date: "`r Sys.Date()`"
---

# 1. Định nghĩa chung của đồ thị con đường truy xuất

Một **đồ thị con đường truy xuất** được định nghĩa là bộ 9-tuple  
> \(G = (N,\,C,\,R,\,C_{\rm đ},\,f,\,g,\,h,\,i,\,j)\)

- **N**: tập nút, mỗi nút \(n_i\) tượng trưng cho một quan hệ (bảng).  
- **C** ⊆ \(N\times N\): tập cung có hướng (FK-edges).  
- **R**: tập quan hệ (tên bảng) trong CSDL.  
- **f: N→R**: gán mỗi nút tới một quan hệ nút.  
- **g: C→R**: gán mỗi cung tới một quan hệ “cung” (bảng chứa FK).  
- **Điều kiện**: \(f(N)\cup g(C)=R\).  
- **Cₑ**: tập con đường truy xuất (thường \(Cₑ=C\)).  
- **h: C→Cₑ**: mỗi cung ứng với một con đường (mô tả truy xuất).  
- **i: Cₑ→ℕ³**: gán cho mỗi con đường bộ \((m,A,M)\) – số bản ghi tối thiểu, trung bình, tối đa.  
- **j: N→{0,1}**: \(j(n_i)=1\) nếu \(n_i\) là nút vào (entry node).

---

# 2. Tập quan hệ và tập nút

## 2.1 Tập quan hệ \(R\)

| Tên bảng                             |
|--------------------------------------|
| TaiKhoan                             |
| KhachHang                            |
| NhanVien                             |
| Tour                                 |
| LichKhoiHanh                         |
| LoTrinh                              |
| KhuyenMai                            |
| HopDong                              |
| HuongDanVien                         |
| LichKhoiHanh_HuongDanVien            |
| PhuongTien                           |
| LichKhoiHanh_PhuongTien              |
| ThanhToan                            |
| YeuCauHoTro                          |
| DanhGia                              |
| DiaDiem                              |
| LoaiDiaDiem                          |
| KhachSan                             |
| LoTrinh_DiaDiem                      |
| LoTrinh_KhachSan                     |

## 2.2 Tập nút \(N\)

| Ký hiệu | Quan hệ nút (bảng)                         |
|:-------:|---------------------------------------------|
| n₁       | TaiKhoan                                    |
| n₂       | KhachHang                                   |
| n₃       | NhanVien                                    |
| n₄       | Tour                                        |
| n₅       | LichKhoiHanh                                |
| n₆       | LoTrinh                                     |
| n₇       | KhuyenMai                                   |
| n₈       | HopDong                                     |
| n₉       | HuongDanVien                                |
| n₁₀      | LichKhoiHanh_HuongDanVien                   |
| n₁₁      | PhuongTien                                  |
| n₁₂      | LichKhoiHanh_PhuongTien                     |
| n₁₃      | ThanhToan                                   |
| n₁₄      | YeuCauHoTro                                 |
| n₁₅      | DanhGia                                     |
| n₁₆      | DiaDiem                                     |
| n₁₇      | LoaiDiaDiem                                 |
| n₁₈      | KhachSan                                    |
| n₁₉      | LoTrinh_DiaDiem                             |
| n₂₀      | LoTrinh_KhachSan                            |

Ánh xạ **f**:  


---

# 3. Tập cung \(C\) và ánh xạ g

Mỗi FK sinh một cung \(c_i\in C\):  

| \(c_i\) | Cung                     | Mô tả FK                                      |
|:-------:|--------------------------|-----------------------------------------------|
| c₁      | n₁ → n₂                  | TaiKhoan.MaKH → KhachHang.MaKH                |
| c₂      | n₁ → n₃                  | TaiKhoan.MaNV → NhanVien.MaNV                 |
| c₃      | n₂ → n₈                  | KhachHang.MaKH → HopDong.MaKH                 |
| c₄      | n₃ → n₈                  | NhanVien.MaNV → HopDong.MaNV                  |
| c₅      | n₈ → n₇                  | HopDong.MaKM → KhuyenMai.MaKM                 |
| c₆      | n₈ → n₅                  | HopDong.MaLich → LichKhoiHanh.MaLich          |
| c₇      | n₈ → n₁₃                 | HopDong.MaHD → ThanhToan.MaHD                 |
| c₈      | n₁₃ → n₂                 | ThanhToan.MaKH → KhachHang.MaKH               |
| c₉      | n₂ → n₁₄                 | YeuCauHoTro.MaKH → KhachHang.MaKH             |
| c₁₀     | n₃ → n₁₄                 | YeuCauHoTro.MaNV → NhanVien.MaNV              |
| c₁₁     | n₂ → n₁₅                 | DanhGia.MaKH → KhachHang.MaKH                 |
| c₁₂     | n₁₅ → n₅                 | DanhGia.MaLich → LichKhoiHanh.MaLich          |
| c₁₃     | n₅ → n₄                  | LichKhoiHanh.MaTour → Tour.MaTour             |
| c₁₄     | n₅ → n₆                  | LoTrinh.MaLich → LichKhoiHanh.MaLich          |
| c₁₅     | n₉ → n₁₀                 | LichKhoiHanh_HuongDanVien.MaLich → …           |
| c₁₆     | n₁₀ → n₉                 | … → HuongDanVien.MaHDV                         |
| c₁₇     | n₅ → n₁₂                 | LichKhoiHanh_PhuongTien.MaLich → LichKhoiHanh |
| c₁₈     | n₁₂ → n₁₁                 | LichKhoiHanh_PhuongTien.MaPT → PhuongTien.MaPT |
| c₁₉     | n₆ → n₁₉                 | LoTrinh_DiaDiem.MaLT → LoTrinh.MaLT           |
| c₂₀     | n₁₉ → n₁₆                | LoTrinh_DiaDiem.MaDD → DiaDiem.MaDD           |
| c₂₁     | n₆ → n₂₀                 | LoTrinh_KhachSan.MaLT → LoTrinh.MaLT           |
| c₂₂     | n₂₀ → n₁₈                | LoTrinh_KhachSan.MaKS → KhachSan.MaKS          |
| c₂₃     | n₁₆ → n₁₇                | DiaDiem.MaLDD → LoaiDiaDiem.MaLDD             |

Ánh xạ **g**:  


---

# 4. Con đường \(C_{đ}\), h và i

- Chọn \(C_{đ}=C\).  
- Với mỗi \(c\in C\), h(c) mô tả “Từ \(f(u)\) → \(f(v)\) qua FK”  
- Ánh xạ **i** gán (m,A,M). Ví dụ:  
  - i(h(c₁))=(0,1,1)  
  - i(h(c₃))=(0,3,N)  
  - i(h(c₆))=(1,1,1)  

---

# 5. Entry-node \(j\)

Chọn **KhachHang (n₂)** làm điểm vào:  