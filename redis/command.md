docker container exec -it redis /bin.sh

# Query

### membuka cli  
redis-cli -h localhost  

### memindah database  
select 0  

### set key value (indempotent)  
set username1 "muchlis cihua"   

### get key  
get username1  
-> "muchlis cihua"  
get username2  
-> (nil)  

### exist  
exist username1  
-> 1  
exist username2  
-> 0  

### del  
del key key2 key3  
-> jumlah row yang didelete  

### append (upsert)  
append username1 " hua"  
-> jumlah huruf  
get username1  
-> "muchlis cihua hua"  

### keys (select key menggunakan regex)  
keys username*  
-> (1) "username1"  

### get range  
getrange username1 0 3  
-> "mucl"  

### mget (mendapatkan value dari beberapa key)  
mget username1 username2  
-> (1) "muchlis"  
(2) (nil)  

### mset  
mset key value key value  

# Expired

ttl username1  
-> -1  

expire username1 360  

ttl username1  
-> 356  

setex username2 "rocky bolboa" 360

# Increment decrement    
inc count  
-> "1"  
inc count  
-> "2"  
dec count  
-> "1"  
incrby 5  
decrby 7  

# Flush  
flushdb  
flushall  

# Bulk Pipeline  
redis-cli --pipe  

file.txt 
(isinya baris set key value)  

cat file.txt | redis-cli -h localhost --pipe  