--Biyografi türünü tür tablosuna ekleyiniz.

SELECT * FROM tur;

INSERT INTO tur(ad)
VALUES('Biyografi');

--Nurettin Belek isimli yazarı yazar tablosuna ekleyiniz.

SELECT * FROM yazar;

INSERT INTO yazar(ad, soyad)
VALUES('Nurettin', 'Belek');

--10B sınıfındaki öğrencileri 10C sınıfına geçirin.

SELECT * FROM ogrenci;

UPDATE ogrenci
SET sinif = '10C'
WHERE sinif = '10B';

--Tüm kitapların puanını 5 puan arttırınız.

SELECT * FROM kitap;

UPDATE kitap
SET puan = puan + 5;

--Adı Mehmet olan tüm yazarları silin.

DELETE FROM yazar
WHERE ad = 'Mehmet';

--Kişisel Gelişim isimli bir tür oluşturun.

INSERT INTO tur(ad)
VALUES('Kişisel Gelişim');

--'Benim Üniversitelerim' isimli kitabın türünü 'Kişisel Gelişim' yapın.

UPDATE kitap
SET turno = 7
WHERE ad = 'Benim Üniversitelerim';

--Öğrenci tablosunu kontrol etmek amaçlı tüm öğrencileri görüntüleyen "ogrencilistesi" adında bir fonksiyon oluşturun.

CREATE FUNCTION public.ogrencilistesi()
RETURNS SETOF ogrenci
LANGUAGE 'sql'
AS $BODY$
SELECT * FROM ogrenci
$BODY$;

SELECT * FROM ogrencilistesi();

--kitap tablosuna yeni kitap eklemek için "ekle" adında bir prosedür oluşturun.

CREATE PROCEDURE public.ekle(
IN k_ad character varying,
IN k_puan integer,
IN k_yazarno integer,
IN k_turno integer)
LANGUAGE 'sql'
AS $BODY$
INSERT INTO kitap(ad, puan, yazarno, turno)
VALUES(k_ad, k_puan, k_yazarno, k_turno)
$BODY$;

CALL public.ekle('haleluya', 30, 5, 3);
DELETE FROM kitap
WHERE ad = 'haleluya';

--Öğrenci noya göre öğrenci silebilmeyi sağlayan "sil" adında bir prosedür oluşturun.

CREATE PROCEDURE public.sil(IN o_no integer)
LANGUAGE 'sql'
AS $BODY$
DELETE FROM ogrenci
WHERE ogrno = o_no
$BODY$;

INSERT INTO ogrenci(ad, soyad, cinsiyet)
VALUES('ezgi', 'kardeş', 'K');

CALL public.sil(11);