# math-computer

--------R로 다음뉴스크롤링하기---------

install.package('rvest')
install.package('stringr')

library(rvest) 
library(stringr)

title = c()      #크롤링한걸 담을 그릇	
press = c()      #	 
time = c()	 # 	
body = c()       #
url = c()        #

url_crawl =  #크롤링하고 싶은 url

for ( i in 1:15){ 		#15페이지까지 긁어오기 위해서 

url_crawl = paste(url_base,i,sep="") #여러페이지를 긁어오기위해 paste함수 사용
t_css = 	#css값들
pt_css = 	#css값들
b_css = 	#css값들

hdoc = read_html(url_crawl) 	#url주소에 해당하는 html을 모두 읽어오는것

t_node = html_nodes(hdoc,t_css)  #css에 해당하는 node를 불러들이는것
				node와 nodes의 차이는 
			   	node의 경우에는 하나의 css만 존재할때 사용
			   	nodes는 여러개의 css가 존재할떄 사용
			   	hdoc에서 t_css에 해당하는 nodes를 가져오겠다.
				
pt_node = html_nodes(hdoc,pt_css)
b_node = httml_nodes(hdoc,b_css)

title_part = html_text(t_node) #node에서 꺽쇠에 해당하는 부분을 다 제거하고 
			  	나머지만 가져오게 하는 명령어

pt_part = html_text(pt_node)
b_part = html_text(b_node)

press_part = str_sub(pt_part,end = -9)  #string에서 필요한 부분만 가져오는 명령어 
					#글자수가 제각각이라서 
					#(어디서 가져올지,start,end)
time_part = str_sub(pt_part,-5)


#b_part 에서는 태그들은 삭제가 되어있지만 나머지 필요없는 부분은 그대로 살아있다
이 부분들을 다듬는 과정

body_part = gsub("\n","",body_part)  		#gsub함수를이용 gsub(바꾸고싶은문자,바꿀문자,문장)
body_part2 = str_trim(body_part,side = "both") 	#특정 스트링을 없애는 부분
body_part3 = str_trim(body_part2,side = "both") #공백을 없애는 명령어
						#없애고 싶은 공백을 고를수있다.
  
url_part = html_attr(t_node , "href") #꺽쇠안에 있는정보중에 내가 원하는 정보를
			               가져올수 있는 명령어
			               태그를 직접 써서 가져올 수 있다.

title = c(title,title_part) #title에다가 title_part를 붙여넣겠다는 의미
press = c(press,press_part)
time = c(time,time_part)
url = c(url,url_part)
}

news = cbind(title,press,time,body,url) #matrix의 형태로 묶어 주는 형태
write.csv(news,"경로") #news라는 변수를 어떤 이름으로 저장을 하겠다.
		       #csv형태로 저장을 하면 그대로 table형태로 불러 올수있다.
