# Ultra Image Server
Bản sửa lại từ docker-imgproxy (https://github.com/shinsenter/docker-imgproxy)

## Cài đặt
```bash
curl -sSL https://get.docker.com | sh
sudo usermod -aG docker $(whoami)
sudo systemctl start docker
sudo systemctl enable docker
apt install docker-compose -y
```

```bash
git clone https://github.com/bibicadotnet/docker-imgproxy-img-bibica-net.git
cd docker-imgproxy-img-bibica-net
docker-compose up -d --build --remove-orphans --force-recreate

#xóa cache
rm -rf cache/
```
## Tạo URL parameters cho ảnh trên Wordpress
Sử dụng Code Snippets tạo 1 file php với nội dung:
 ```bash
function jetpack_photon_custom($attr, $attachment, $size) {
	
	 if ($size === 'thumbnail') {
        $attr['src'] .= '?w=300';
	} 
	else if ($size === 'medium') {
        $attr['src'] .= '?w=768';
	}
	else if ($size === 'full') {
        $attr['src'] .= '?w=768';
    }	
	else if ($size === 'medium_large') {
        $attr['src'] .= '?w=768';
    }	
	else if ($size === 'large') {
        $attr['src'] .= '?w=768';
    }	
	else if ($size === '1536x1536') {
        $attr['src'] .= '?w=768';
    }
	else if ($size === '2048x2048') {
        $attr['src'] .= '?w=768';
    }

    return $attr;
}

add_filter('wp_get_attachment_image_attributes', 'jetpack_photon_custom', 999 , 3);
function replace_text($text) {
	$text = str_replace('.jpg" alt', '.jpg?w=768" alt', $text);
	$text = str_replace('.jpeg" alt', '.jpeg?w=768" alt', $text);
	$text = str_replace('.png" alt', '.png?w=768" alt', $text);
	$text = str_replace('.gif" alt', '.gif?w=768" alt', $text);
	$text = str_replace('.webp" alt', '.webp?w=768" alt', $text);
	$text = str_replace('.avif" alt', '.avif?w=768" alt', $text);
	$text = str_replace('.bmp" alt', '.bmp?w=768" alt', $text);
	
	return $text;
}
add_filter('the_content', 'replace_text');

```
## Sử dụng
Link ảnh bên trong sẽ được thêm ?w=300 cho các ảnh thumbnail, các định dạng khác sẽ thêm ?w=768
