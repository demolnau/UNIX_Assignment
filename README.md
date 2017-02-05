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
sort -c sorted_snp_position.txt 
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

### gjoin does not work
gjoin -1 1 -2 1 -a 1 sorted_transposed_genotypes.txt snp_position_sorted.txt > joined_genotype_snp.txt














