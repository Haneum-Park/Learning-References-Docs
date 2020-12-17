## Rails 조회수 구현[Gem: impressionist]

### 조회수 기능(IP Check 포함)

1.  `rails g scaffold post title content:text` 스캐폴드 생성

2.  `gem 'impressionist'` 추가

3.  `bundle install`

4.  `rails generate impressionist`

5.  `raks db:migrate`

6.  `app/models/post.rb` (게시판 관련 model파일)에서 다음 내용 추가

    ```ruby
    class Post < ApplicationRecord
      ...
      is_impressionable
      ...
    end
    ```

7.  조회수가 노출되길 원하는 view에 다음 변수를 추가

    ```erb
    <% @posts.each do |post| %>
        ...
        <td><%= "#{post.impressionist_count} views" %></td>
        ...
    <% end %>
    ```



###  **Impressionist Cache 컬럼 추가 및** 조회수 높은 순으로 정렬하기

1.  `rails g migration AddImpressionsCountTo(모델명) impressions_count:int`

2.  `rake db:migrate`

3.  정렬을 하고자 하는 대상의 Model에서, 다음 내용을 추가

    ```ruby
    class Post < ApplicationRecord
      ...
      is_impressionable :counter_cache => true, :unique => true
    end
    ```

4.  정렬을 하고자 하는 대상의 Controller에서, 다음 내용을 추가

    ```ruby
    class PostsController < ApplicationController
      ...
      def index
        ...
        @posts = Post.order("impressions_count DESC")
      end
      ...
    end
    ```



## References

1.  Git - impressionist : `https://github.com/charlotte-ruby/impressionist`
2.  Stackoverflow : `https://stackoverflow.com/questions/4815713/simple-hit-counter-for-page-views-in-rails`
3.  Stackoverflow : `https://stackoverflow.com/questions/23174338/counting-page-views-using-impressionist-gem-ruby-on-rails`

