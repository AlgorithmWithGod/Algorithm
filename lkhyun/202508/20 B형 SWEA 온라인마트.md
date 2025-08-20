```java
import java.util.*;

class UserSolution
{
    static class Product implements Comparable<Product>{
        int mID;
        int mPrice;

        Product(int mID, int mPrice){
            this.mID = mID;
            this.mPrice = mPrice;
        }
        @Override
        public int compareTo(Product other){
            if(this.mPrice == other.mPrice){
                return Integer.compare(this.mID, other.mID);
            }else{
                return Integer.compare(this.mPrice, other.mPrice);
            }
        }
    }
    
    static class ProductInfo{
        int mCategory;
        int mCompany;
        
        ProductInfo(int mCategory, int mCompany){
            this.mCategory = mCategory;
            this.mCompany = mCompany;
        }
    }
    
    static Map<Integer, ProductInfo> productInfoByID;
    static Map<Integer, Product> productByID;
    static TreeSet<Product>[][] productByCateCom;
    static int[][] diff;
    
    public void init()
    {
        productInfoByID = new HashMap<>();
        productByID = new HashMap<>();
        productByCateCom = new TreeSet[6][6];
        for (int i = 1; i <= 5; i++) {
            for (int j = 1; j <= 5; j++) {
                productByCateCom[i][j] = new TreeSet<>();
            }
        }
        diff = new int[6][6];
    }

    public int sell(int mID, int mCategory, int mCompany, int mPrice)
    {
        Product newProduct = new Product(mID, mPrice - diff[mCategory][mCompany]);
        ProductInfo newProductInfo = new ProductInfo(mCategory, mCompany);
        
        productInfoByID.put(mID, newProductInfo);
        productByID.put(mID, newProduct);
        productByCateCom[mCategory][mCompany].add(newProduct);

        return productByCateCom[mCategory][mCompany].size();
    }

    public int closeSale(int mID)
    {
        if(!productInfoByID.containsKey(mID)) return -1;

        ProductInfo info = productInfoByID.get(mID);
        Product product = productByID.get(mID);
        
        int realPrice = product.mPrice + diff[info.mCategory][info.mCompany];
        
        productByCateCom[info.mCategory][info.mCompany].remove(product);
        productInfoByID.remove(mID);
        productByID.remove(mID);
        
        return realPrice;
    }

    public int discount(int mCategory, int mCompany, int mAmount)
    {
        diff[mCategory][mCompany] -= mAmount;
        
        TreeSet<Product> categoryProducts = productByCateCom[mCategory][mCompany];
        
        while (!categoryProducts.isEmpty()) {
            Product first = categoryProducts.first();
            if (first.mPrice + diff[mCategory][mCompany] <= 0) {
                categoryProducts.pollFirst();
                productInfoByID.remove(first.mID);
                productByID.remove(first.mID);
            } else {
                break;
            }
        }
        
        return categoryProducts.size();
    }

    Solution.RESULT show(int mHow, int mCode)
    {
        Solution.RESULT res = new Solution.RESULT();
        res.cnt = 0;
        
        TreeSet<Product> candidates = new TreeSet<>((p1, p2) -> {
            int price1 = p1.mPrice + diff[productInfoByID.get(p1.mID).mCategory][productInfoByID.get(p1.mID).mCompany];
            int price2 = p2.mPrice + diff[productInfoByID.get(p2.mID).mCategory][productInfoByID.get(p2.mID).mCompany];
            
            if (price1 == price2) {
                return Integer.compare(p1.mID, p2.mID);
            }
            return Integer.compare(price1, price2);
        });
        
        for (int i = 1; i <= 5; i++) {
            if (mHow == 1 && i != mCode) continue;
            
            for (int j = 1; j <= 5; j++) {
                if (mHow == 2 && j != mCode) continue;
                
                TreeSet<Product> categoryProducts = productByCateCom[i][j];
                if (categoryProducts.isEmpty()) continue;
                
                for (Product p : categoryProducts) {
                    int realPrice = p.mPrice + diff[i][j];
                    if (realPrice <= 0) continue;
                    
                    if (candidates.size() < 5) {
                        candidates.add(p);
                    } else {
                        Product last = candidates.last();
                        int lastPrice = last.mPrice + diff[productInfoByID.get(last.mID).mCategory][productInfoByID.get(last.mID).mCompany];
                        
                        if (realPrice < lastPrice || (realPrice == lastPrice && p.mID < last.mID)) {
                            candidates.pollLast();
                            candidates.add(p);
                        } else {
                            break;
                        }
                    }
                }
            }
        }
        
        for (Product p : candidates) {
            res.IDs[res.cnt++] = p.mID;
        }
        
        return res;
    }
}
```
