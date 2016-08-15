# suggestion - 蘇介吾 105/08/16

##建立專案步驟
```
rails g scaffold topic title description:text
rails g model vote topic:references (等同 topic_id:integer)
rake db:migrate
```
##控制器加入
```
  #######################################
  def upvote
    @topic = Topic.find(params[:id])
    @topic.votes.create
    redirect_to(topics_path)
  end
  #######################################
```

##視圖加入
```
  #######################################
<td><%= topic.votes.count %></td>
<td><%= button_to '投我', upvote_topic_path(topic), method: :post %></td>
  #######################################
```

##路由加入
```
  #######################################
 resources :topics do
    member do
      post 'upvote'
    end 
  end 

  root 'topics#index'
  #######################################
```
  
##執行
```
rails s  => OK
```
