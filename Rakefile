desc "Fetch product"
task :fetch_products do

  require 'nokogiri'
  require 'open-uri'
  require 'csv'
  
  CSV.open('data/dump.csv', 'ab') do |csv|

    csv << ["nombre", "rubro", "marca", "proveedor", "precio"]

    1.upto(22) do |n|

      puts "Leyendo página #{n}..."
      products = Nokogiri::HTML(open("http://precioscuidados.com/pagina/#{n}/"))
      products.css('div.product').each do |product|
        product_price = product.css('.info-prod .price').text.delete("$ ").gsub(",", ".").to_f
        product_info  = product.css('.info li div.col-2')
        csv << [product_info[0].text, product_info[1].text, product_info[2].text, product_info[3].text, product_price]
      end
    
    end
    
    puts "=================================================================="
    puts "Data exportada en data/dump.csv."

  end
  
end
