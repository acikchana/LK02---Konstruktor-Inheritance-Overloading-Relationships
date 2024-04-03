# LK02---Konstruktor-Inheritance-Overloading-Relationships
Nama : Acik Imtia Chana
NIM : 235150701111038

package Kendaraan;

import java.util.Scanner;

class kendaraan {
    public String platNomor;
    public int jumlahPenumpang;
    public int kapasitas;
    public Driver driver;

    public kendaraan(String pn, int max){
        this.platNomor = pn;
        this.jumlahPenumpang = 0;
        this.kapasitas = max;

    }

    public void showplatNomor(){
        System.out.println("Plat nomor: " + this.platNomor);
    }
    public void shownamaDriver(){
        System.out.println("Nama Driver anda: " + this.driver.nama);
    }
    public void cekPenumpang(){
        System.out.println("Penumpang saat ini: "+this.jumlahPenumpang);
    }

    public void penumpangNaik(int naik){
        System.out.println("Penumpang naik : "+naik);
        int current = this.jumlahPenumpang;
        if (current + naik > this.kapasitas){
            System.out.println("Mohon maaf penumpang melebihi kapasitas");
        }
        else{
            this.jumlahPenumpang += naik;
            System.out.println("penumpang berhasil naik");
        }
        cekPenumpang();
    }

    public void penumpangNaik(int naik, String genderPenumpang){
        int current = this.jumlahPenumpang;
        if(current + naik > this.kapasitas){
            System.out.println("Mohon maaf penumpang melebihi kapasitas");
        } else {
            this.jumlahPenumpang += naik;
            System.out.println("Penumpang " + genderPenumpang + " berhasil naik " + naik);
        }
        cekPenumpang();
    }

    public void penumpangTurun(int turun){
        System.out.println("Penumpang turun: "+turun);
        int current = this.jumlahPenumpang;
        if (current - turun < 0){
            System.out.println("Mohon maaf tidak ada penumpang yang turun");
        }
        else{
            this.jumlahPenumpang -= turun;
            System.out.println("penumpang berhasil turun " + turun);
        }
        cekPenumpang();
    }
    
}

public class Bus extends kendaraan {
    private boolean Toilet;
    private int totalHalte;

    public Bus(String platNomor, boolean Toilet, int kapasitas, int totalHalte) {
        super(platNomor, kapasitas);
        this.Toilet = Toilet;
        this.totalHalte = totalHalte;
        System.out.println("=============================");
        System.out.println("Halo saya objek dari kelas Bus dengan plat nomor : " + this.platNomor);
    }

    public void setToilet(boolean Toilet){
        this.Toilet = Toilet;
    }
    public boolean Toilet(){
        return Toilet;
    }
    public int gettotalHalte(){
        return totalHalte;
    }

    public void berhentiDiHalte(int nomorHalte) {
        System.out.println("Bus " + this.platNomor + " berhenti di halte ke-" + nomorHalte);
    }

}

public class Truk extends kendaraan {
    private int muatanMax;

    public Truk(String platNomor, int kapasitas, int muatanMax) {
        super(platNomor, kapasitas);
        this.muatanMax = muatanMax;
        System.out.println("Truk dengan plat nomor : " + this.platNomor);
    }

    public void setmuatanMax(int muatanMax){
        this.muatanMax = muatanMax;
    }

    public int getmuatanMax(){
        return muatanMax;
    }
    
}

class Driver {
    public String nama;
    public int noSim;

    public Driver(String nama){
        this.nama = nama;
    }
    public void setnoSim(int noSim){
        this.noSim = noSim;
    }
}

public class App {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        System.out.println("Selamat datang di program kendaraan!");

        int pilihanKendaraan = 0;
        int pilihan = 0;

        while (pilihanKendaraan != 1 && pilihanKendaraan !=2) {
            System.out.println("\n=== Pilih Kendaraan ===");
            System.out.println("1. Bus");
            System.out.println("2. Truk");
            System.out.print("\nMasukkan pilihan anda: ");
            pilihanKendaraan = input.nextInt();
            input.nextLine();
            
            
            if (pilihanKendaraan == 1) {
                Bus bus = new Bus("N 3456 YZ", true , 30, 8);
                Driver d1 = new Driver("Mahmud");
                bus.driver = d1;
                bus.shownamaDriver();
                bus.showplatNomor();
                bus.Toilet();
                bus.gettotalHalte();
                bus.berhentiDiHalte(pilihan);
                
                while (pilihan != 4) {
                    System.out.println("\nMenu:");
                    System.out.println("1. Penumpang Naik");
                    System.out.println("2. Penumpang Turun");
                    System.out.println("3. Cek Jumlah Penumpang");
                    System.out.println("4. Keluar");
                    System.out.print("\nMasukkan pilihan anda: ");

                    pilihan = input.nextInt();
                    switch (pilihan) {
                        case 1:
                        System.out.println("\nPilih gender penumpang:");
                        System.out.println("1. Perempuan");
                        System.out.println("2. Laki-Laki");
                        System.out.print("\nMasukkan Pilihan Anda: ");
                        int pilihanPenumpang = input.nextInt();
                        System.out.println("=======================================");
                        System.out.print("Masukkan jumlah penumpang yang akan naik: ");
                        int naik = input.nextInt();
                        switch (pilihanPenumpang) {
                            case 1:
                            bus.penumpangNaik(naik, "Perempuan");
                            break;
                            case 2:
                            bus.penumpangNaik(naik, "Laki-Laki");
                            break;
                            default:
                            System.out.println("Pilihan tidak valid.");
                            break;
                        }
                            case 2:
                            System.out.print("Jumlah penumpang yang akan turun: ");
                            int turun = input.nextInt();
                            bus.penumpangTurun(turun);
                            break;
                            case 3:
                            bus.cekPenumpang();
                            break;
                            case 4:
                            System.out.println("Terima kasih telah menggunakan layanan kami!");
                            break;
                            default:
                            System.out.println("Pilihan tidak valid");
                            }
                        }
                
            } else if (pilihanKendaraan == 2) {
                Truk truk = new Truk("N 3456 LM", 700, 3);
                Driver d2 = new Driver("Yudiono");
                truk.driver = d2;
                truk.shownamaDriver();
                truk.showplatNomor();
                System.out.println("Kapasitas muatan truk: " + truk.getmuatanMax() + " ton");
        
                while (pilihan != 4) {
                    System.out.println("\nMenu:");
                    System.out.println("1. Penumpang Naik");
                    System.out.println("2. Penumpang Turun");
                    System.out.println("3. Cek Jumlah Penumpang");
                    System.out.println("4. Keluar");
                    System.out.print("Masukkan pilihan anda: ");
                    pilihan = input.nextInt();
                    
                    switch (pilihan) {
                        case 1:
                        System.out.println("\nPilih gender penumpang:");
                        System.out.println("1. Perempuan");
                        System.out.println("2. Laki-Laki");
                        System.out.print("\nPilihan Anda: ");
                        int pilihanPenumpang = input.nextInt();
                        System.out.print("Jumlah penumpang yang akan naik: ");
                        int naik = input.nextInt();
                        switch (pilihanPenumpang) {
                            case 1:
                                truk.penumpangNaik(naik, "Perempuan");
                                break;
                            case 2:
                                truk.penumpangNaik(naik, "Laki-Laki");
                                break;
                            default:
                                System.out.println("Pilihan tidak valid.");
                        }break;
                            case 2:
                                System.out.print("Masukkan jumlah penumpang yang akan turun: ");
                                int turun = input.nextInt();
                                truk.penumpangTurun(turun);
                                break;
                            case 3:
                                truk.cekPenumpang();
                                break;
                            case 4:
                                System.out.println("Terima kasih telah menggunakan layanan kami!");
                                break;
                            default:
                                System.out.println("Pilihan tidak valid");
                            }
                        }
                    }
                    input.close();
                }
    }
}

