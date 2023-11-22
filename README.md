#include<iostream>
#include<string>
#include<iomanip>
using namespace std;
class NhanVien
{
private:
	int maNV;
	string hoTen, ngaySinh, diaChi;
	float luongCB, phuCap, thucLinh;
public:
	void NHAP()
	{
		cout << "Nhap ma nhan vien: ";
		cin >> maNV;
		cout << "Nhap ho va ten nhan vien:";
		cin.ignore();
		getline(cin, hoTen);
		cout << "Nhap ngay sinh nhan vien:";
		getline(cin, ngaySinh);
		cout << "Nhap dia chi cua nhan vien:";
		getline(cin, diaChi);
		cout << "Nhap luong co ban cua nhan vien:";
		cin >> luongCB;
		cout << "Nhap phu cap cua nhan vien:";
		cin >> phuCap;
		thucLinh = luongCB + phuCap;
	}

	void XUAT()
	{
		cout << maNV << "\t|" << hoTen << "\t\t|" << ngaySinh << "\t|" << diaChi << "\t\t|" << luongCB << "\t\t|" << phuCap << "\t\t|" << thucLinh << "\n";
	}

	int get_maNV()
	{
		return maNV;
	}

	float get_luongCB()
	{
		return luongCB;
	}

	float get_phuCap()
	{
		return phuCap;
	}

	void set_luongCB(float lcb)
	{
		luongCB = lcb;
	}

	void set_phuCap(float pc)
	{
		phuCap = pc;
	}

	void set_diaChi(string dc)
	{
		diaChi = dc;
	}
};
void nhap_dsnv(NhanVien nv[], int n)
{
	for (int i = 0; i < n; i++)
	{
		cout << "Nhap nhan vien thu" << i + 1 << "\n";
		nv[i].NHAP();
	}
	cout << "Da nhap xong danh sach gom " << n << " nhan vien.\n";
}
void xuat_dsnv(NhanVien nv[], int n)
{
	cout << "Danh sach nhan vien cua cong ty nhu sau:\n";
	cout << "Ma nv\t|Ho ten\t\t|Ngay sinh\t|Dia chi\t\t|Luong Cb\t\t|Phu cap\t\t|Thuc linh\n";
	for (int i = 0; i < n; i++)
		nv[i].XUAT();
}
void xuat_dsnv_thuclinh_max(NhanVien nv[], int n)
{
	cout << "Danh sch ngan vien co thuc linh cao nhat cong ty:\n";
	float max = 0;
	for (int i = 0; i < n; i++)
	{
		if (nv[i].get_luongCB() + nv[i].get_phuCap() > max) max = nv[i].get_luongCB() + nv[i].get_phuCap();
	}
	for (int i = 0; i < n; i++)
	{
		if (nv[i].get_luongCB() + nv[i].get_phuCap() == max) nv[i].XUAT();
	}
}

void xuat_dsnv_thuclinh_min(NhanVien nv[], int n)
{
	cout << "Danh sch ngan vien co thuc linh thap nhat cong ty:\n";
	float min = nv[0].get_luongCB() + nv[0].get_phuCap();
	for (int i = 1; i < n; i++)
	{
		if (nv[i].get_luongCB() + nv[i].get_phuCap() < min) min = nv[i].get_luongCB() + nv[i].get_phuCap();
	}
	for (int i = 0; i < n; i++)
	{
		if (nv[i].get_luongCB() + nv[i].get_phuCap() == min) nv[i].XUAT();
	}
}
int main()
{
	int soLuong;
	NhanVien nv[1000];
	cout << "Nhap so luong nhan vien cua cong ty:";
	cin >> soLuong;
	nhap_dsnv(nv, soLuong);
	xuat_dsnv(nv, soLuong);
	xuat_dsnv_thuclinh_max(nv, soLuong);
	xuat_dsnv_thuclinh_min(nv, soLuong);
}
