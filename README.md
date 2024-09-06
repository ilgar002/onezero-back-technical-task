# BackEnd Task

## Təsvir
Bu tapşırıqda sizdən iki endpoint yaratmaq tələb olunur. Lazım olan məlumatlar **data.json** faylında yerləşdirilib. Tapşırığın əsas məqsədi məhsulların məlumatlarını sorğulayıb, onlara mümkün endirimlər tətbiq edərək nəticələri qaytarmaqdır. Tapşırıq `node.js` istifadə edilərək yazılmalıdır.

## Endpoints:

### 1. Bütün menyunun qaytarılması:
Bu endpoint bütün menyunu geri qaytarmalıdır.
- Əlavə olaraq, `date` adında parametr qəbul etməlidir. Əgər `date` verilibsə, hər bir məhsul üçün həmin tarixə uyğun endirim tətbiq edilməli və məhsullar qaytarılmalıdır.

### 2. ID ilə məhsulun qaytarılması:
Bu endpoint verilən ID-yə uyğun **menu-item** tapıb geri qaytarmalıdır.
- Bu endpoint də əlavə olaraq `date` parametrini qəbul etməlidir. Əgər bu parametr verilibsə, həmin tarixə uyğun məhsulun endirimi hesablanmalı və məhsul qaytarılmalıdır.


## Əlavə Məlumatlar:
- **priceSell**: Məhsulun satış qiyməti (endirim burada tətbiq edilir).
#### Məhsul məlumatlarının içərisində **rate** adında obyekt mövcuddur və bu obyekt məhsulun endirim vəziyyətini təyin edir. Bu obyektin xüsusiyyətləri:

- **rate.isEnabled**: Məhsula endirim tətbiq olunub-olunmadığını göstərir. True olarsa endirim tətbiq edilir, false olarsa edilməz.
- **rate.isFixed**: Endirimin növünü göstərir. Əgər false olarsa, **rate.amount** faiz olaraq tətbiq edilir. Əgər true olarsa, **rate.amount** sabit (fixed) məbləğdə tətbiq olunur.
- **rate.schedule.isActive**: Endirimin müəyyən vaxt aralığında aktiv olduğunu ifadə edir.
    - **True şərtində**: Endirim **schedule.from** və **schedule.to** tarixləri arasında aktiv olmalıdır. Əgər endpointə `date` parametri göndərilibsə, həmin `date`in bu aralığda olub-olmadığı yoxlanılır. Əgər olarsa, endirim tətbiq edilir, yoxsa tətbiq olunmur.
- **rate.schedule.weekdays**: weekdays daxilində həftənin günləri qeyd edilib ve **isWorking** adında keyləri mövcuddur. Əgər endpointə göndərilən `date` schedule tarixləri arasındadırsa, o zaman həftənin günləridə nəzərə alınmalıdır mütləq şəkildə. Endpointə göndərilən `date`-in həftənin hansı gününə aid olması tapılıb, həmin günün **schedule.weekdays** daxilində `isWorking` dəyəri və saatları (from, to) yoxlanıb ona uyğun olaraq discount tətbiq edilməlidir.
  

## Tapşırığın icrası üçün addımlar:
1. İlk endpoint bütün menyunu geri qaytarmalıdır.
2. İkinci endpoint verilən ID-yə uyğun məhsul tapıb geri qaytarmalıdır.
3. Hər iki endpoint əlavə olaraq `date` parametrini qəbul edə bilməlidir və endirimlərin tətbiqi üçün yuxarıda qeyd olunan qaydalar əsasında hesablamalar aparılmalıdır.