# hash 一致性算法实现
from dubbo HashConsistentloadbalance
```java
public class HashConsistent {

	public static void main(String []args) {
		int replicaNumber = 16;
		 for (int i = 0; i < replicaNumber / 4; i++) {
         	//这里存在问题，测试时多个节点始终往一个节点跑
             byte[] digest = md5("This/is/atest" + i);//md5(Str + 0,1,2,3..39)
             System.out.println("this is test i:" + i);
             for (int h = 0; h < 4; h++) {
                 long m = hash(digest, h);//hash(digest,0)/hash(digest,1)hash(digest,2)/hash(digest,3)
                 System.out.println(m);
             }
         }
	}

	private static byte[] md5(String value) {
        MessageDigest md5;
        try {
            md5 = MessageDigest.getInstance("MD5");
        } catch (NoSuchAlgorithmException e) {
            throw new IllegalStateException(e.getMessage(), e);
        }
        md5.reset();
        byte[] bytes = null;
        try {
            bytes = value.getBytes("UTF-8");
        } catch (UnsupportedEncodingException e) {
            throw new IllegalStateException(e.getMessage(), e);
        }
        md5.update(bytes);
        return md5.digest();
    }

	private static long hash(byte[] digest, int number) {
        return (((long) (digest[3 + number * 4] & 0xFF) << 24)
                | ((long) (digest[2 + number * 4] & 0xFF) << 16)
                | ((long) (digest[1 + number * 4] & 0xFF) << 8)
                | (digest[0 + number * 4] & 0xFF))
                & 0xFFFFFFFFL;
    }
}
```
