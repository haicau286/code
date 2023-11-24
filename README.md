#include <iostream>
#include <string>
#include <sstream>
#include <algorithm>
using namespace std;
class LinkedList {
private:
    struct NhanVien {
        string mNV, ten, ngaysinh;
        double luongCoBan, phucap, luongThucLinh; 
        NhanVien* next;
        void in();
        void nhap();
    };
    NhanVien* head;
public:
    LinkedList() : head(NULL) {}
    ~LinkedList();
    void themNhanVien();
    void xoaNhanVien(string mNV);
    void inds();
    NhanVien* timNhanVienTheoMa(string mNV);
    void timNhanVien();
    void sapXep();
    void suaThongTinNhanVien(string mNV);
};
void LinkedList::NhanVien::in() {
    cout << "-----------------------------------------\n";
    cout << "Ma nhan vien :" << mNV << endl;
    cout << "Ten nhan vien :" << ten << endl;
    cout << "Ngay sinh :" << ngaysinh << endl;
    cout << "Luong Co ban  :" <<luongCoBan << endl;
    cout << "Phu cap :"<<  phucap << endl;
	cout << "Tong Luong  :" <<luongThucLinh << endl; 
    cout << "------------------------------------------\n";
}
void LinkedList::NhanVien::nhap() {
    cout << "Nhap ma nhan vien : ";
    cin.ignore();
    getline(cin, mNV);
    cout << "Nhap ten nhan vien : ";
    getline(cin, ten);
    cout << "Nhap ngay thang nam sinh : ";
    getline(cin, ngaysinh);
    cout << "Nhap luong co ban : ";
    cin>>luongCoBan;
    cout<< "Nhap phu cap: ";
	cin>>phucap;
	luongThucLinh = luongCoBan+phucap;
}
LinkedList::~LinkedList() {
    while (head != NULL) {
        NhanVien* temp = head;
        head = head->next;
        delete temp;
    }
}
void LinkedList::themNhanVien() {
    NhanVien* newEmployee = new NhanVien;
    newEmployee->nhap();
    while (timNhanVienTheoMa(newEmployee->mNV) != NULL) {
        cout << "Ma nhan vien da ton tai. Vui long nhap lai: ";
        cin.ignore();
        getline(cin, newEmployee->mNV);
    }
    newEmployee->next = head;
    head = newEmployee;
}
void LinkedList::xoaNhanVien(string mNV) {
    if (head == NULL) {
        cout << "Danh sach rong. Khong the xoa.\n";
        return;
    }
    if (head->mNV == mNV) {
        NhanVien* newHead = head->next;
        delete head;
        head = newHead;
        cout << "Da xoa nhan vien co ma " << mNV << endl;
        return;
    }
    NhanVien* current = head;
    while (current->next != NULL && current->next->mNV != mNV) {
        current = current->next;
    }
    if (current->next != NULL) {
        NhanVien* temp = current->next;
        current->next = current->next->next;
        delete temp;
        cout << "Da xoa nhan vien co ma " << mNV << endl;
    } 
	else {
    	 cout << "Khong tim thay nhan vien co ma " << mNV << endl;
        }
}
void LinkedList::inds() {
    NhanVien* current = head;
    while (current != NULL) {
        current->in();
        current = current->next;
    }
}
LinkedList::NhanVien* LinkedList::timNhanVienTheoMa(string mNV) {
    NhanVien* current = head;
    while (current != NULL) {
        if (current->mNV == mNV) {
            return current;
        }
        current = current->next;
    }
    return NULL;
}
void LinkedList::timNhanVien() {
    cout << "Chon phuong thuc tim kiem:\n";
    cout << "1. Theo ma nhan vien\n";
    cout << "0. Tro ve menu chinh\n";
    int choice;
    cin >> choice;
    switch (choice) {
        case 1: {
            string mNV;
            cout << "Nhap ma nhan vien can tim : ";
            cin.ignore();
            getline(cin, mNV);
            if (timNhanVienTheoMa(mNV)== NULL)
            cout << "Khong tim thay nhan vien co ma: "<<mNV<<endl;
            else timNhanVienTheoMa(mNV)->in();
            break;
        }
        case 0:
            break;
        default:
            cout << "Lua chon khong hop le. Vui long nhap lai.\n";
    }
}
void LinkedList::sapXep() {
    NhanVien* current = head;
    NhanVien* nextNhanVien;
    while (current != NULL) {
        nextNhanVien = current->next;
        while (nextNhanVien != NULL) {
            if (current->mNV.compare(nextNhanVien->mNV) > 0) {
                swap(current->mNV, nextNhanVien->mNV);
                swap(current->ten, nextNhanVien->ten);
                swap(current->ngaysinh, nextNhanVien->ngaysinh);
                swap(current->luongCoBan, nextNhanVien->luongCoBan);
                swap(current->phucap, nextNhanVien->phucap);
                swap(current->luongThucLinh, nextNhanVien->luongThucLinh);
            }
            nextNhanVien = nextNhanVien->next;
        }
        current = current->next;
    }
    cout << "Danh sach nhan vien sau khi sap xep theo ma nv: " << "\n";
    inds();
}
void LinkedList::suaThongTinNhanVien(string criteria) {
    cout << "Chon tieu chi sua thong tin:\n";
    cout << "1. Theo ma nhan vien\n";
    cout << "2. Theo ten nhan vien\n";
    cout << "3. Theo luong co ban \n";
    cout << "4. Theo ngay thang nam sinh\n";
    cout << "5. Theo phu cap \n"; 
    cout << "0. Tro ve menu chinh\n";
    int choice;
    cin >> choice;
    NhanVien*current= timNhanVienTheoMa(criteria);
        switch (choice) {
            case 1:
                cout << "Nhap ma nhan vien moi: ";
                cin.ignore();
                getline(cin, current->mNV);
                break;
            case 2:
                cout << "Nhap ten moi: ";
				cin.ignore();
				getline(cin, current->ten);               
                break;
            case 3:
                cout << "Nhap luong co ban moi: ";
                cin >> current->luongCoBan;
                break;
            case 4:
                cout << "Nhap ngay thang nam sinh moi: ";
                cin.ignore();
                getline(cin, current->ngaysinh);
                break;
            case 5:
			    cout << "Nhap phu cap moi: ";
				cin >> current->phucap;
				break; 
            case 0:
                return;
            default:
                cout << "Lua chon khong hop le. Vui long nhap lai.\n";
                return;
        }

}
int main() {
    LinkedList danhSachNhanVien;
    while (1) {
        cout << "---------------MENU---------------\n";
        cout << "1. Nhap thong tin nhan vien\n";
        cout << "2. Hien thi toan bo danh sach nhan vien\n";
        cout << "3. Tim kiem nhan vien\n";
        cout << "4. Sap xep nhan vien\n";
        cout << "5. Sua thong tin nhan vien\n";
        cout << "6. Xoa nhan vien\n ";
        cout << "0. Thoat !\n";
        cout << "------------------------------------\n";
        cout << "Nhap lua chon: ";
        int lc;
        cin >> lc;
        switch (lc) {
            case 1:
                danhSachNhanVien.themNhanVien();
                break;
            case 2:
                danhSachNhanVien.inds();
                break;
            case 3:
                danhSachNhanVien.timNhanVien();
                break;
            case 4: {
                cout << "Chon tieu chi sap xep:\n";
                cout << "1. Theo ma\n";
                cout << "0. Tro ve menu chinh\n";
                int choice;
                cin >> choice;
                switch (choice) {
                    case 1:
                        danhSachNhanVien.sapXep();
                        break;
                    case 0:
                        break;
                    default:
                        cout << "Lua chon khong hop le. Vui long nhap lai.\n";
                }
                break;
            }
            case 5: {
                string mNV;
                cout << "Nhap ma nhan vien can sua thong tin: ";
                cin.ignore();
                getline(cin, mNV);
                danhSachNhanVien.suaThongTinNhanVien(mNV);
                break;
            }
            case 6: {
                string mNV;
                cout << "Nhap ma nhan vien can xoa: ";
                cin.ignore();
                getline(cin, mNV);
                danhSachNhanVien.xoaNhanVien(mNV);
                break;
            }  	
            case 0:
                return 0;
            default:
                cout << "Lua chon khong hop le. Vui long nhap lai.\n";
        }
    }
    return 0;
}
