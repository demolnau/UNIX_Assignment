# UNIX_Assignment
Maize and teosinte data sets are first pulled from the fang\_et\_al\_genotypes.txt. They are then joined with snp\_position.txt and excess data is removed so that there is only SNP_ID, Chromosome, Position and genotype data is left. Each set is separated further by chromosome and sorted by position. All files named sorted\_maize* or sorted\_teosinte* are sorted by increasing snp position.All files named reverse\_sorted\_maize* or reverse\_sorted\_teosinte* are sorted in reverse order and all "?" in the file have been replaced with "-".


#### find the number of columns in fang\_et\_al_genotypes.txt
awk -F "\t" '{print NF; exit}' fang*
#### find the number of rows in fang\_et\_al\_genotypes.txt
cut -f 1 fang\_et\_al\_genotypes.txt| wc -l
#### find out how many unique groups are within fang
cut -f 3 fang\_et\_al\_genotypes.txt |sort| uniq -c

##MAIZE

####
grep 'ZMM' fang\_et\_al\_genotypes.txt > maize_genotype.txt

head -n 1 fang\_et\_al\_genotypes.txt > header.txt

cat header.txt maize\_genotype.txt > header\_maize\_genotype.txt

####Transpose header+maize genotype file 

awk -f transpose.awk header\_maize\_genotype.txt > transposed\_header\_maize\_genotypes.txt

cut -f 1 transposed\_header\_maize\_genotypes.txt | wc

cut -f 1 transposed\_header\_maize\_genotypes.txt

#### sort transposed_header_maize_genotypes text file 

tail -n +4 transposed\_header\_maize\_genotypes.txt| sort -k1,1 > sorted\_transposed\_header\_maize\_genotypes.txt

cut -f 1 sorted\_transposed\_header\_maize\_genotypes.txt | wc

cut -f 1 sorted\_transposed\_header\_maize\_genotypes.txt 

####check to see if snp_position.txt is sorted
sort -c snp\_position.txt

#### sort the snp_position.txt file
head -n 1 snp\_position.txt > snp\_header.txt

tail -n +2 snp\_position.txt | sort -k1,1 > sorted\_snp_position.txt

cut -f 1 sorted\_snp\_position.txt

#### join sorted sip files and sorted transposed header+maize genotype data.
join -t $'\t' -1 1 -2 1 sorted\_snp\_position.txt 
sorted\_transposed\_header\_maize\_genotypes.txt > joined\_maize.txt

####Add snp headers back
cat snp_header.txt joined\_maize.txt > joined\_header\_maize\_genotype\_snp.txt

cat joined\_header\_maize\_genotype\_snp.txt| cut -f 1-16| head

####word count the lines for all the documents
wc -l snp_position.txt sorted\_snp\_position.txt 

transposed\_header\_maize\_genotypes.txt 

sorted\_transposed\_header\_maize\_genotypes.txt joined\_genotype\_snp.txt
 
#### check how many columns are in joined_maize.txt
awk -F "\t" '{print NF; exit}' joined\_maize.txt 

### Cut out unnecessary information
cut -f 1,3,4,16- joined\_header\_maize\_genotype\_snp.txt | head | cut -f 1-10

cut -f 1,3,4,16- joined\_header\_maize\_genotype\_snp.txt > reordered\_maize\_genotype\_snp.txt

#### How many SNPs are on each maize chromosome
cut -f 2 reordered\_maize\_genotype\_snp.txt |sort -n | uniq -c

awk '$2 == 1' reordered\_maize\_genotype\_snp.txt  > maize\_chromosome\_1.txt

cat maize\_chromosome\_1.txt|head

cut -f 2 maize\_chromosome\_1.txt| sort| uniq -c

awk '$2 == 2' reordered\_maize\_genotype\_snp.txt  > maize\_chromosome\_2.txt

awk '$2 == 3' reordered\_maize\_genotype\_snp.txt  > maize\_chromosome\_3.txt

awk '$2 == 4' reordered\_maize\_genotype\_snp.txt  > maize\_chromosome\_4.txt

awk '$2 == 5’ reordered\_maize\_genotype\_snp.txt  > maize\_chromosome\_5.txt

awk '$2 == 6' reordered\_maize\_genotype\_snp.txt  > maize\_chromosome\_6.txt

awk '$2 == 7’ reordered\_maize\_genotype\_snp.txt  > maize\_chromosome\_7.txt

awk '$2 == 8’ reordered\_maize\_genotype\_snp.txt  > maize\_chromosome\_8.txt

awk '$2 == 9’ reordered\_maize\_genotype\_snp.txt  > maize\_chromosome\_9.txt

awk '$2 == 10' reordered\_maize\_genotype\_snp.txt  > maize\_chromosome\_10.txt

cut -f 2 maize\_chromosome\_10.txt| sort| uniq -c

### Increasing position sort of maize chromosome SNPs

sort -k3,3n maize\_chromosome\_1.txt|head| cut -f 1-3

sort -k3,3n maize\_chromosome\_1.txt >sorted\_maize\_chromosome\_1.txt

cat sorted\_maize\_chromosome\_1.txt|head |cut -f 1-6|column -t        
sort -k3,3n maize\_chromosome\_2.txt > sorted\_maize\_chromosome\_2.txt

sort -k3,3n maize\_chromosome\_3.txt > sorted\_maize\_chromosome\_3.txt

sort -k3,3n maize\_chromosome\_4.txt > sorted\_maize\_chromosome_4.txt

sort -k3,3n maize\_chromosome\_5.txt > sorted\_maize\_chromosome\_5.txt

sort -k3,3n maize\_chromosome\_6.txt > sorted\_maize\_chromosome\_6.txt

sort -k3,3n maize\_chromosome\_7.txt > sorted\_maize\_chromosome\_7.txt

sort -k3,3n maize\_chromosome\_8.txt > sorted\_maize\_chromosome\_8.txt

sort -k3,3n maize\_chromosome\_9.txt > sorted\_maize\_chromosome\_9.txt

sort -k3,3n maize\_chromosome\_10.txt > sorted\_maize\_chromosome\_10.txt



###Decreasing position order and replace ‘?’ with ‘-‘
sort -k3,3nr maize\_chromosome\_10.txt|head| cut -f 1-10

sort -k3,3nr maize\_chromosome\_10.txt| sed 's/?/-/g'| head| cut -f 1-10

sort -k3,3nr maize\_chromosome\_10.txt| sed ’s/?/-/g’> reverse\_maize\_chromosome\_10.txt

sort -k3,3nr maize\_chromosome\_9.txt| sed 's/?/-/g'> reverse\_maize\_chromosome\_9.txt

sort -k3,3nr maize\_chromosome\_8.txt| sed 's/?/-/g'> reverse\_maize\_chromosome\_8.txt

sort -k3,3nr maize\_chromosome\_7.txt| sed 's/?/-/g'> reverse\_maize\_chromosome\_7.txt

sort -k3,3nr maize\_chromosome\_7.txt| sed 's/?/-/g'> reverse\_maize\_chromosome\_6.txt

sort -k3,3nr maize\_chromosome\_6.txt| sed 's/?/-/g'> reverse\_maize\_chromosome\_6.txt

sort -k3,3nr maize\_chromosome\_5.txt| sed 's/?/-/g'> reverse\_maize\_chromosome\_5.txt

sort -k3,3nr maize\_chromosome\_4.txt| sed 's/?/-/g'> reverse\_maize\_chromosome\_4.txt

sort -k3,3nr maize\_chromosome\_3.txt| sed 's/?/-/g'> reverse\_maize\_chromosome\_3.txt

sort -k3,3nr maize\_chromosome\_2.txt| sed 's/?/-/g'> reverse\_maize\_chromosome\_2.txt

sort -k3,3nr maize\_chromosome\_1.txt| sed 's/?/-/g'> reverse\_maize\_chromosome\_1.txt





##TEOSINTE
####pull teosinte data out of the file
grep 'ZMP' fang\_et\_al\_genotypes.txt > teosinte\_genotype.txt

cat header.txt teosinte\_genotype.txt > header\_teosinte\_genotype.txt

#### transpose teosinte file with its headers

awk -f transpose.awk header\_teosinte\_genotype.txt > transposed\_header\_teosinte\_genotypes.txt

cut -f 1 transposed\_header\_teosinte\_genotypes.txt | wc

cut -f 1 transposed\_header\_teosinte\_genotypes.txt

tail -n +4 transposed\_header\_teosinte\_genotypes.txt | sort -k1,1 > sorted\_transposed\_header\_teosinte\_genotypes.txt

#### join sorted sip files and sorted transposed header+teosinte genotype data.
join -t $'\t' -1 1 -2 1 sorted\_snp\_position.txt sorted\_transposed\_header\_teosinte\_genotypes.txt > joined\_teosinte.txt

#### Add back the snap headers to joined teosinte file
cat snp\_header.txt joined\_teosinte.txt > joined\_header\_teosinte\_genotype\_snp.txt
cat joined\_header\_teosinte\_genotype\_snp.txt| cut -f 1-16| head

####word count the lines for all the documents
wc -l snp\_position.txt sorted\_snp\_position.txt transposed\_header\_maize\_genotypes.txt sorted\_transposed\_header\_maize\_genotypes.txt joined\_genotype\_snp.txt  transposed\_header\_teosinte\_genotypes.txt sorted\_transposed\_header\_teosinte\_genotypes.txt joined\_teosinte.txt

#### check to see how many columns are in joined teosinte text file
awk -F "\t" '{print NF; exit}' joined\_teosinte.txt 

### Cut out unnecessary information
cut -f 1,3,4,16- joined\_header\_teosinte\_genotype\_snp.txt | head | cut -f 1-10| column -t

cut -f 1,3,4,16- joined\_header\_teosinte\_genotype\_snp.txt > reordered\_teosinte\_genotype\_snp.txt

#### How many SNPs are on each teosinte chromosome
cut -f 2 reordered\_teosinte\_genotype\_snp.txt |sort -n | uniq -c

awk '$2 == 1' reordered\_teosinte\_genotype\_snp.txt  > teosinte\_chromosome\_1.txt

cat teosinte\_chromosome\_1.txt |head|cut -f 1-10

cut -f 2 teosinte\_chromosome\_1.txt| sort| uniq -c

awk '$2 == 2' reordered\_teosinte\_genotype\_snp.txt  > teosinte\_chromosome\_2.txt

awk '$2 == 3' reordered\_teosinte\_genotype\_snp.txt  > teosinte\_chromosome\_3.txt

awk '$2 == 4' reordered\_teosinte\_genotype\_snp.txt  > teosinte\_chromosome\_4.txt

awk '$2 == 5' reordered\_teosinte\_genotype\_snp.txt  > teosinte\_chromosome\_5.txt

awk '$2 == 6' reordered\_teosinte\_genotype\_snp.txt  > teosinte\_chromosome\_6.txt

awk '$2 == 7' reordered\_teosinte\_genotype\_snp.txt  > teosinte\_chromosome\_7.txt

awk '$2 == 8' reordered\_teosinte\_genotype\_snp.txt  > teosinte\_chromosome\_8.txt

awk '$2 == 9' reordered\_teosinte\_genotype\_snp.txt  > teosinte\_chromosome\_9.txt

awk '$2 == 10' reordered\_teosinte\_genotype\_snp.txt  > teosinte\_chromosome\_10.txt

cut -f 2 teosinte\_chromosome\_10.txt| sort| uniq -c

### Increasing position sort of teosinte chromosome SNPs

sort -k3,3n teosinte\_chromosome\_1.txt|head| cut -f 1-3

sort -k3,3n teosinte\_chromosome\_1.txt >sorted\_teosinte\_chromosome\_1.txt

cat sorted\_teosinte\_chromosome\_1.txt| head |cut -f 1-6|column -t        
sort -k3,3n teosinte\_chromosome\_2.txt > sorted\_teosinte\_chromosome\_2.txt

sort -k3,3n teosinte\_chromosome\_3.txt > sorted\_teosinte\_chromosome\_3.txt

sort -k3,3n teosinte\_chromosome\_4.txt > sorted\_teosinte\_chromosome\_4.txt

sort -k3,3n teosinte\_chromosome\_5.txt > sorted\_teosinte\_chromosome\_5.txt

sort -k3,3n teosinte\_chromosome\_6.txt > sorted\_teosinte\_chromosome\_6.txt

sort -k3,3n teosinte\_chromosome\_7.txt > sorted\_teosinte\_chromosome\_7.txt

sort -k3,3n teosinte\_chromosome\_8.txt > sorted\_teosinte\_chromosome\_8.txt

sort -k3,3n teosinte\_chromosome\_9.txt > sorted\_teosinte\_chromosome\_9.txt

sort -k3,3n teosinte\_chromosome\_10.txt > sorted\_teosinte\_chromosome\_10.txt

###Decreasing position order and replace ‘?’ with ‘-‘

sort -k3,3nr teosinte\_chromosome\_10.txt | head| cut -f 1-10

sort -k3,3nr teosinte\_chromosome\_10.txt| sed 's/?/-/g'| head| cut -f 1-10

sort -k3,3nr teosinte\_chromosome\_10.txt| sed 's/?/-/g'> reverse\_teosinte\_chromosome\_10.txt

sort -k3,3nr teosinte\_chromosome\_9.txt| sed 's/?/-/g'> reverse\_teosinte\_chromosome\_9.txt

sort -k3,3nr teosinte\_chromosome\_8.txt| sed 's/?/-/g'> reverse\_teosinte\_chromosome\_8.txt

sort -k3,3nr teosinte\_chromosome\_7.txt| sed 's/?/-/g'> reverse\_teosinte\_chromosome\_7.txt

sort -k3,3nr teosinte\_chromosome\_7.txt| sed 's/?/-/g'> reverse\_teosinte\_chromosome\_6.txt

sort -k3,3nr teosinte\_chromosome\_6.txt| sed 's/?/-/g'> reverse\_teosinte\_chromosome\_6.txt

sort -k3,3nr teosinte\_chromosome\_5.txt| sed 's/?/-/g'> reverse\_teosinte\_chromosome\_5.txt

sort -k3,3nr teosinte\_chromosome\_4.txt| sed 's/?/-/g'> reverse\_teosinte\_chromosome\_4.txt

sort -k3,3nr teosinte\_chromosome\_3.txt| sed 's/?/-/g'> reverse\_teosinte\_chromosome\_3.txt

sort -k3,3nr teosinte\_chromosome\_2.txt| sed 's/?/-/g'> reverse\_teosinte\_chromosome\_2.txt

sort -k3,3nr teosinte\_chromosome\_1.txt| sed 's/?/-/g'> reverse\_teosinte\_chromosome\_1.txt







