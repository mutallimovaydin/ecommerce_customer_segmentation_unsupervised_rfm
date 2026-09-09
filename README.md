# Technical Documentation: Online Retail Customer Segmentation

## 1. Data Cleaning & Feature Preparation
- **Missing Value Handling:** CustomerID sütununda olan 135,080 boş sətir silindi.
- **Filtering:** 'C' ilə başlayan ləğv olunmuş sifarişlər (cancellations) və mənfi/sıfır `Quantity`/`UnitPrice` dəyərləri təmizləndi.
- **Skewness Correction:** RFM dəyərlərinin sağa çəp (right-skewed) paylanmasını normallaşdırmaq üçün `np.log1p()` transformasiyası tətbiq edildi.
- **Scaling:** Məsafə əsaslı alqoritmlər üçün bütün xüsusiyyətlərə `StandardScaler` tətbiq olundu.

## 2. Outlier Detection
- **Method:** `DBSCAN` istifadə olundu.
- **Justification:** Aşırı yüksək xərcləyən wholesale/topdan satıcı müştərilər K-Means mərkəzlərini deforma etməsin deyə 5% kənar dəyər olaraq təmizləndi.

## 3. Model Selection & Validation
- **K-Means Evaluation:** $k \in [2, 10]$ diapazonunda yoxlanıldı.
- **Elbow Method:** Inertia qrafikində dirsək nöqtəsi $k=4$ kimi müəyyən olundu.
- **Silhouette Score:** Ən yüksək klaster ayrılması $k=4$ olduqda əldə edildi (Silhouette Score ~ 0.38-0.42).
- **Hierarchical Clustering Comparison:** Dendrogram kəsim nöqtəsi də 4 əsas klaster strukturu ilə üst-üstə düşdü.

## 4. Business Segment Mapping
- **Cluster 0:** Champions (Yüksək F, M; Aşağı R)
- **Cluster 1:** Loyal Customers (Orta-Yüksək F, M; Aşağı R)
- **Cluster 2:** At-Risk / Need Attention (Aşağı R, M; Yüksək F)
- **Cluster 3:** Lost / Hibernating (Çox aşağı F, M; Çox yüksək R)
