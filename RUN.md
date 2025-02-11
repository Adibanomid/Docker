#
وقتی که ساخته میشود شما به صورت مستقیم نمیتوانید دسترسی داشته باشید
به همین خاطر باید ابتدا به صورت لوکال وارد شوید یوزر ها را بسازید



**چون env به صورت .env هستش به صورت خودکار صدا زده میشه مگر اسم دیگه گزاشته باشید**
docker compose -f docker-compose.base.yaml -p geobizz-btools up -d

# for base image  for developers
docker compose -f docker-compose.libnahad.yaml -p geobizz-libnahad up -d 


# for geobizz image
docker compose -f docker-compose.geobizz.yaml -p geobizz up -d