# UNIX_Assignment

#### how to open a program using a linus operating system
xdg-open README.md





#### find the number of columns in fang_et_al_genotypes.txt
awk -F "\t" '{print NF; exit}' fang*
#### transpose fang_et_al_genotypes.txt
awk -f transpose.awk fang_et_al_genotypes.txt > transposed_genotypes.txt
####make sure that there is the same number of rows as there was columns
cut -f 1 transposed_genotypes.txt | wc
#### sort transposed_genotypes text file 
sort -k1,1 transposed_genotypes.txt > sorted_transposed_genotypes.txt
####check to see if snp_position.txt is sorted
sort -c snp_position.txt
#### sort the snp_position.txt file
sort -k1,1 snp_position.txt > sorted_snp_position.txt

####check to see if sort worked 
sort -k1,1 -c sorted_snp_position.txt 
##PROBLEM!! NOT SORTED!

cut -f 1 sorted_transposed_genotypes.txt

cut -f 1 snp_position.txt

cut -f 1 sorted_snp_position.txt

####join the sorted transposed genotypes data with sorted snp position text
join -1 1 -2 1 sorted_transposed_genotypes.txt sorted_snp_position.txt > joined_genotype_snp.txt

####cut the first column and see what it is spitting out. WHY IS THIS NOT THE SAME AS the sorted_snp_position.txt?
cut -f 1 joined_genotype_snp.txt 


####word count the lines for all the documents
wc -l snp_position.txt snp_position_sorted.txt transposed_genotypes.txt sorted_transposed_genotypes.txt joined_genotype_snp.txt 




####
grep 'ZMM' fang_et_al_genotypes.txt > maize_genotype.txt
head -n 1 fang_et_al_genotypes.txt > header.txt
cat header.txt maize_genotype.txt > header_maize_genotype.txt
####Transpose header+maize genotype file 
awk -f transpose.awk header_maize_genotype.txt > transposed_header_maize_genotypes.txt
cut -f 1 transposed_header_maize_genotypes.txt | wc
cut -f 1 transposed_header_maize_genotypes.txt
#### sort transposed_header_maize_genotypes text file 

tail -n +4 transposed_header_maize_genotypes.txt| sort -k1,1 > sorted_transposed_header_maize_genotypes.txt
cut -f 1 sorted_transposed_header_maize_genotypes.txt | wc
cut -f 1 sorted_transposed_header_maize_genotypes.txt 

####check to see if snp_position.txt is sorted
sort -c snp_position.txt

#### sort the snp_position.txt file
head -n 1 snp_position.txt > snp_header.txt
tail -n +2 snp_position.txt | sort -k1,1 > sorted_snp_position.txt
cut -f 1 sorted_snp_position.txt

#### join sorted sip files and sorted transposed header+maize genotype data.
join -t $'\t' -1 1 -2 1 sorted_snp_position.txt sorted_transposed_header_maize_genotypes.txt > joined_maize.txt

###Add snp headers back
cat snp_header.txt joined_maize.txt > joined_header_maize_genotype_snp.txt
cat joined_header_maize_genotype_snp.txt| cut -f 1-16| head

####word count the lines for all the documents
wc -l snp_position.txt sorted_snp_position.txt transposed_header_maize_genotypes.txt sorted_transposed_header_maize_genotypes.txt joined_genotype_snp.txt
 
#### check how many columns are in joined_maize.txt
 awk -F "\t" '{print NF; exit}' joined_maize.txt 

### Cut out unnecessary information
cut -f 1,3,4,16- joined_header_maize_genotype_snp.txt | head | cut -f 1-10

cut -f 1,3,4,16- joined_header_maize_genotype_snp.txt > reordered_maize_genotype_snp.txt

#### How many SNPs are on each maize chromosome
cut -f 2 reordered_maize_genotype_snp.txt |sort -n | uniq -c

awk '$2 == 1' reordered_maize_genotype_snp.txt  > maize_chromosome_1.txt

cat maize_chromosome_1.txt|head

cut -f 2 maize_chromosome_1.txt| sort| uniq -c

awk '$2 == 2' reordered_maize_genotype_snp.txt  > maize_chromosome_2.txt

awk '$2 == 3' reordered_maize_genotype_snp.txt  > maize_chromosome_3.txt

awk '$2 == 4' reordered_maize_genotype_snp.txt  > maize_chromosome_4.txt

awk '$2 == 5’ reordered_maize_genotype_snp.txt  > maize_chromosome_5.txt

awk '$2 == 6' reordered_maize_genotype_snp.txt  > maize_chromosome_6.txt

awk '$2 == 7’ reordered_maize_genotype_snp.txt  > maize_chromosome_7.txt

awk '$2 == 8’ reordered_maize_genotype_snp.txt  > maize_chromosome_8.txt

awk '$2 == 9’ reordered_maize_genotype_snp.txt  > maize_chromosome_9.txt

awk '$2 == 10' reordered_maize_genotype_snp.txt  > maize_chromosome_10.txt

cut -f 2 maize_chromosome_10.txt| sort| uniq -c

### Increasing position sort of maize chromosome SNPs

sort -k3,3n maize_chromosome_1.txt|head| cut -f 1-3

sort -k3,3n maize_chromosome_1.txt >sorted_maize_chromosome_1.txt

cat sorted_maize_chromosome_1.txt|head |cut -f 1-6|column -t        
sort -k3,3n maize_chromosome_2.txt > sorted_maize_chromosome_2.txt

sort -k3,3n maize_chromosome_3.txt > sorted_maize_chromosome_3.txt

sort -k3,3n maize_chromosome_4.txt > sorted_maize_chromosome_4.txt

sort -k3,3n maize_chromosome_5.txt > sorted_maize_chromosome_5.txt

sort -k3,3n maize_chromosome_6.txt > sorted_maize_chromosome_6.txt

sort -k3,3n maize_chromosome_7.txt > sorted_maize_chromosome_7.txt

sort -k3,3n maize_chromosome_8.txt > sorted_maize_chromosome_8.txt

sort -k3,3n maize_chromosome_9.txt > sorted_maize_chromosome_9.txt

sort -k3,3n maize_chromosome_10.txt > sorted_maize_chromosome_10.txt



###Decreasing position order and replace ‘?’ with ‘-‘
sort -k3,3nr maize_chromosome_10.txt|head| cut -f 1-10

sort -k3,3nr maize_chromosome_10.txt| sed 's/?/-/g'| head| cut -f 1-10

sort -k3,3nr maize_chromosome_10.txt| sed ’s/?/-/g’> reverse_maize_chromosome_10.txt

sort -k3,3nr maize_chromosome_9.txt| sed 's/?/-/g'> reverse_maize_chromosome_9.txt

sort -k3,3nr maize_chromosome_8.txt| sed 's/?/-/g'> reverse_maize_chromosome_8.txt

sort -k3,3nr maize_chromosome_7.txt| sed 's/?/-/g'> reverse_maize_chromosome_7.txt

sort -k3,3nr maize_chromosome_7.txt| sed 's/?/-/g'> reverse_maize_chromosome_6.txt

sort -k3,3nr maize_chromosome_6.txt| sed 's/?/-/g'> reverse_maize_chromosome_6.txt

sort -k3,3nr maize_chromosome_5.txt| sed 's/?/-/g'> reverse_maize_chromosome_5.txt

sort -k3,3nr maize_chromosome_4.txt| sed 's/?/-/g'> reverse_maize_chromosome_4.txt

sort -k3,3nr maize_chromosome_3.txt| sed 's/?/-/g'> reverse_maize_chromosome_3.txt

sort -k3,3nr maize_chromosome_2.txt| sed 's/?/-/g'> reverse_maize_chromosome_2.txt

sort -k3,3nr maize_chromosome_1.txt| sed 's/?/-/g'> reverse_maize_chromosome_1.txt





#TEOSINTE
####pull teosinte data out of the file
grep 'ZMP' fang_et_al_genotypes.txt > teosinte_genotype.txt

cat header.txt teosinte_genotype.txt > header_teosinte_genotype.txt

#### transpose teosinte file with its headers

awk -f transpose.awk header_teosinte_genotype.txt > transposed_header_teosinte_genotypes.txt

cut -f 1 transposed_header_teosinte_genotypes.txt | wc

cut -f 1 transposed_header_teosinte_genotypes.txt

tail -n +4 transposed_header_teosinte_genotypes.txt | sort -k1,1 > sorted_transposed_header_teosinte_genotypes.txt

#### join sorted sip files and sorted transposed header+teosinte genotype data.
join -t $'\t' -1 1 -2 1 sorted_snp_position.txt sorted_transposed_header_teosinte_genotypes.txt > joined_teosinte.txt

#### Add back the snap headers to joined teosinte file
cat snp_header.txt joined_teosinte.txt > joined_header_teosinte_genotype_snp.txt
cat joined_header_teosinte_genotype_snp.txt| cut -f 1-16| head

####word count the lines for all the documents
wc -l snp_position.txt sorted_snp_position.txt transposed_header_maize_genotypes.txt sorted_transposed_header_maize_genotypes.txt joined_genotype_snp.txt  transposed_header_teosinte_genotypes.txt sorted_transposed_header_teosinte_genotypes.txt joined_teosinte.txt

#### check to see how many columns are in joined teosinte text file
awk -F "\t" '{print NF; exit}' joined_teosinte.txt 

### Cut out unnecessary information
cut -f 1,3,4,16- joined_header_teosinte_genotype_snp.txt | head | cut -f 1-10| column -t

cut -f 1,3,4,16- joined_header_teosinte_genotype_snp.txt > reordered_teosinte_genotype_snp.txt

#### How many SNPs are on each teosinte chromosome
cut -f 2 reordered_teosinte_genotype_snp.txt |sort -n | uniq -c

awk '$2 == 1' reordered_teosinte_genotype_snp.txt  > teosinte_chromosome_1.txt

cat teosinte_chromosome_1.txt |head|cut -f 1-10

cut -f 2 teosinte_chromosome_1.txt| sort| uniq -c

awk '$2 == 2' reordered_teosinte_genotype_snp.txt  > teosinte_chromosome_2.txt

awk '$2 == 3' reordered_teosinte_genotype_snp.txt  > teosinte_chromosome_3.txt

awk '$2 == 4' reordered_teosinte_genotype_snp.txt  > teosinte_chromosome_4.txt

awk '$2 == 5' reordered_teosinte_genotype_snp.txt  > teosinte_chromosome_5.txt

awk '$2 == 6' reordered_teosinte_genotype_snp.txt  > teosinte_chromosome_6.txt

awk '$2 == 7' reordered_teosinte_genotype_snp.txt  > teosinte_chromosome_7.txt

awk '$2 == 8' reordered_teosinte_genotype_snp.txt  > teosinte_chromosome_8.txt

awk '$2 == 9' reordered_teosinte_genotype_snp.txt  > teosinte_chromosome_9.txt

awk '$2 == 10' reordered_teosinte_genotype_snp.txt  > teosinte_chromosome_10.txt

cut -f 2 teosinte_chromosome_10.txt| sort| uniq -c

### Increasing position sort of teosinte chromosome SNPs

sort -k3,3n teosinte_chromosome_1.txt|head| cut -f 1-3

sort -k3,3n teosinte_chromosome_1.txt >sorted_teosinte_chromosome_1.txt

cat sorted_teosinte_chromosome_1.txt| head |cut -f 1-6|column -t        
sort -k3,3n teosinte_chromosome_2.txt > sorted_teosinte_chromosome_2.txt

sort -k3,3n teosinte_chromosome_3.txt > sorted_teosinte_chromosome_3.txt

sort -k3,3n teosinte_chromosome_4.txt > sorted_teosinte_chromosome_4.txt

sort -k3,3n teosinte_chromosome_5.txt > sorted_teosinte_chromosome_5.txt

sort -k3,3n teosinte_chromosome_6.txt > sorted_teosinte_chromosome_6.txt

sort -k3,3n teosinte_chromosome_7.txt > sorted_teosinte_chromosome_7.txt

sort -k3,3n teosinte_chromosome_8.txt > sorted_teosinte_chromosome_8.txt

sort -k3,3n teosinte_chromosome_9.txt > sorted_teosinte_chromosome_9.txt

sort -k3,3n teosinte_chromosome_10.txt > sorted_teosinte_chromosome_10.txt

###Decreasing position order and replace ‘?’ with ‘-‘

sort -k3,3nr teosinte_chromosome_10.txt | head| cut -f 1-10

sort -k3,3nr teosinte_chromosome_10.txt| sed 's/?/-/g'| head| cut -f 1-10

sort -k3,3nr teosinte_chromosome_10.txt| sed 's/?/-/g'> reverse_teosinte_chromosome_10.txt

sort -k3,3nr teosinte_chromosome_9.txt| sed 's/?/-/g'> reverse_teosinte_chromosome_9.txt

sort -k3,3nr teosinte_chromosome_8.txt| sed 's/?/-/g'> reverse_teosinte_chromosome_8.txt

sort -k3,3nr teosinte_chromosome_7.txt| sed 's/?/-/g'> reverse_teosinte_chromosome_7.txt

sort -k3,3nr teosinte_chromosome_7.txt| sed 's/?/-/g'> reverse_teosinte_chromosome_6.txt

sort -k3,3nr teosinte_chromosome_6.txt| sed 's/?/-/g'> reverse_teosinte_chromosome_6.txt

sort -k3,3nr teosinte_chromosome_5.txt| sed 's/?/-/g'> reverse_teosinte_chromosome_5.txt

sort -k3,3nr teosinte_chromosome_4.txt| sed 's/?/-/g'> reverse_teosinte_chromosome_4.txt

sort -k3,3nr teosinte_chromosome_3.txt| sed 's/?/-/g'> reverse_teosinte_chromosome_3.txt

sort -k3,3nr teosinte_chromosome_2.txt| sed 's/?/-/g'> reverse_teosinte_chromosome_2.txt

sort -k3,3nr teosinte_chromosome_1.txt| sed 's/?/-/g'> reverse_teosinte_chromosome_1.txt







