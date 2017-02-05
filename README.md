# UNIX_Assignment

awk -F "\t" '{print NF; exit}' fang*
awk -f transpose.awk fang_et_al_genotypes.txt > transposed_genotypes.txt
cut -f 1 transposed_genotypes.txt | wc

xdg-open README.md

sort -k1,1 transposed_genotypes.txt > sorted_transposed_genotypes.txt
sort -k1,1 snp_positions.txt > sorted_snp_position.txt

sort -c snp_position.txt
sort -c sorted_snp_position.txt

cut -f 1 sorted_transposed_genotypes.txt|wc
cut -f 1 snp_position.txt|wc
cut -f 1 snp_position_sorted.txt |wc

join -1 1 -2 1 sorted_transposed_genotypes.txt snp_position_sorted.txt > joined_genotype_snp.txt
cut -f 1 joined_genotype_snp.txt | wc

wc -l snp_position.txt snp_position_sorted.txt transposed_genotypes.txt sorted_transposed_genotypes.txt joined_genotype_snp.txt 

# gjoin does not work
gjoin -1 1 -2 1 -a 1 sorted_transposed_genotypes.txt snp_position_sorted.txt > joined_genotype_snp.txt














