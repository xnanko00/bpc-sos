# bpc-sos projekt

V tomto projekte sme zmenšovali operačný systém a tu budú uvedené skripty ktoré nám k tomu pomohli

tento skript bol prevzatý
```bash
function remove {
  for targer in "$@" ; do
    rm -fv $target
done
}

DIR1=$HOME/all_modules.txt
DIR2=$HOME/current_modules.txt

find /lib/modules/$(uname −r) -type f -name '*.ko*' > $DIR1

for module in `lsmod | cut -f1 -d" " | tail -n +2`; do
  filename=`modinfo $module -n`
  echo "$filename" >> $DIR2
done

sort $DIR1 | uniq > file1.sorted
sort $DIR2 | uniq > file2.sorted

remove `comm -23 file1.sorted file2.sorted`
remove `find /usr/lib/firmware -atime +2`

find /boot -maxdepth 1 -type f -name *rescue* - delete
grub2-mkconfig -o /boot/grub2/grub.cfg

rm 
```

následne sme zmazali jazykové balíčky tak že sme v zložke `/usr/share/locale` postupne mazali balíčky príkazom rm -rfv a* až po z* okrem e* kde sme zmazali len všetky okrem používaných en_US


