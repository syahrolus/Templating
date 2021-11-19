CREATE DATABASE qudsdev;
USE qudsdev;

DROP TABLE instruktur;
DROP TABLE peserta;


CREATE TABLE tb_peserta(
id_peserta INT(4) PRIMARY KEY AUTO_INCREMENT,
id_admin INT (4),
username VARCHAR(255),
email VARCHAR (255),
pass VARCHAR(255),
address VARCHAR(255),
no_hp VARCHAR(255),
gender VARCHAR(255),
tgl_lahir DATETIME,


   CONSTRAINT FK_admin FOREIGN KEY (id_admin)
    REFERENCES tb_admin(id_admin)
);

CREATE TABLE tb_admin(
id_admin INT(4) PRIMARY KEY AUTO_INCREMENT,
username VARCHAR(255),
email VARCHAR (255),
pass VARCHAR(255)
);


CREATE TABLE tb_instruktur(
id_instruktur INT(4) PRIMARY KEY AUTO_INCREMENT,
id_admin INT (4),
id_bidang INT(4),
username VARCHAR(255),
pass VARCHAR(255), 
address VARCHAR (255),
gender VARCHAR(255),
alamat_peserta VARCHAR(255),
foto VARCHAR(255),
tgl_lahir DATETIME,


	  
 CONSTRAINT FK_bidang FOREIGN KEY (id_bidang)
    REFERENCES tb_bidang(id_bidang),
    
    CONSTRAINT FK_admin FOREIGN KEY (id_admin)
    REFERENCES tb_admin(id_admin)

);

CREATE TABLE tb_kategori_event(
id_kategori INT(4) PRIMARY KEY AUTO_INCREMENT,
id_admin INT (4),
nama_kategori VARCHAR(255),

   CONSTRAINT FK_admin FOREIGN KEY (id_admin)
    REFERENCES tb_admin(id_admin)
);


CREATE TABLE tb_tugas(
id_tugas INT(4) PRIMARY KEY AUTO_INCREMENT,
id_admin INT (4),
id_soal INT(4),
id_record INT(4),
tgl_tugas DATETIME,
deadline_tugas DATETIME,
kode CHAR(5),
keterangan VARCHAR(255),


CONSTRAINT FK_admin FOREIGN KEY (id_admin)
    REFERENCES tb_admin(id_admin),
    
    
CONSTRAINT FK_soal FOREIGN KEY (id_soal)
    REFERENCES tb_soal(id_soal),
    
    CONSTRAINT FK_record FOREIGN KEY (id_record)
    REFERENCES tb_record(id_record)



);

`qudsdev`
CREATE TABLE tb_hasil_tugas(
id_hasil_tugas INT(4) PRIMARY KEY AUTO_INCREMENT,
id_admin INT(4),
id_tugas INT(4),
isi_hasil_tugas VARCHAR(255),
tgl_submit VARCHAR(255),
poin INT(15),
keterangan VARCHAR(255),
status_tugas VARCHAR(255),


   CONSTRAINT FK_admin FOREIGN KEY (id_admin)
    REFERENCES tb_admin(id_admin),
    
    
   CONSTRAINT FK_tugas FOREIGN KEY (id_tugas)
    REFERENCES tb_tugas(id_tugas)

);

CREATE TABLE tb_event(
id_event INT(4) PRIMARY KEY AUTO_INCREMENT,
id_admin INT (4),
id_instruktur INT(4),
id_kategori INT(4),
harga INT(18),
deskripsi VARCHAR(255),
tgl_mulai DATETIME,
tgl_akhir DATETIME,



	  
 CONSTRAINT FK_kategori FOREIGN KEY (id_kategori)
    REFERENCES tb_kategori_event(id_kategori),
    
    CONSTRAINT FK_admin FOREIGN KEY (id_admin)
    REFERENCES tb_admin(id_admin),
    
    CONSTRAINT FK_instruktur FOREIGN KEY (id_instruktur)
    REFERENCES tb_instruktur(id_instruktur)
    
    


);

CREATE TABLE tb_record(
id_record INT(4) PRIMARY KEY AUTO_INCREMENT,
id_event INT (4),
id_peserta INT(4),
id_admin INT (4),
status_peserta VARCHAR(255),


	  
 CONSTRAINT FK_peserta FOREIGN KEY (id_peserta)
    REFERENCES tb_peserta(id_peserta),
    
    CONSTRAINT FK_admin FOREIGN KEY (id_admin)
    REFERENCES tb_admin(id_admin),
    
    CONSTRAINT FK_event FOREIGN KEY (id_event)
    REFERENCES tb_event(id_event)
    

);


CREATE TABLE tb_bidang(
id_bidang INT(4) PRIMARY KEY AUTO_INCREMENT,
id_admin INT (4),
nama_bidang VARCHAR(255),

   CONSTRAINT FK_admin FOREIGN KEY (id_admin)
    REFERENCES tb_admin(id_admin)
);


CREATE TABLE tb_soal(
id_soal INT(4) PRIMARY KEY AUTO_INCREMENT,
id_admin INT (4),
id_event INT (4),
isi_soal VARCHAR(255),
keterangan VARCHAR(255),



CONSTRAINT FK_admin FOREIGN KEY (id_admin)
    REFERENCES tb_admin(id_admin),

    CONSTRAINT FK_event FOREIGN KEY (id_event)
    REFERENCES tb_event(id_event)

);





