8 Resources
Mani, S. K., Hussain, M., Hasan, S., Zhou, K., Zou, X., & Sekar, V. (2025). Securing public cloud networks with efficient role-based micro-segmentation. USENIX NSDI ’25.

Rose, S., Borchert, O., Mitchell, S., & Connelly, S. (2020). Zero Trust Architecture (NIST SP 800-207). National Institute of Standards and Technology.

CISA. (2023). Zero Trust Maturity Model v2.0. U.S. Department of Homeland Security.

NSA. (2021–2023). Embracing a Zero Trust Security Model and pillar guidance (e.g., User pillar v1.1). National Security Agency.

Liu, R., Lin, Y., Yang, X., Ng, S. H., Divakaran, D. M., & Dong, J. S. (2022). Inferring phishing intention via webpage appearance and dynamics: A deep vision-based approach. USENIX Security ’22.

Haq, Q. E., Sadiq, S., Shafique, A., & Farooq, M. (2024). Detecting phishing URLs using a 1D-CNN. Applied Sciences, 14(22), 10086.

Anti-Phishing Working Group (APWG). (2025). Phishing Activity Trends Report: Q2 2025.

Microsoft Threat Intelligence. (2024, Nov 4). How Microsoft Defender for Office 365 innovated to address QR-code phishing attacks. Microsoft Security Blog.

Comparison notes
The Goal
ZTA: Reduce breach impact and lateral movement via continuous verification (identity, device, traffic) and least-privilege segmentation.

Phishing Detection: Stop initial compromise by catching malicious emails/URLs/pages before credential theft or malware delivery.

Dependencies
ZTA: Strong identity inventory, device posture signals, reliable flow/auth telemetry.

Phishing: Fresh, de-duplicated datasets; time-split evaluation; safe headless rendering for content-based detection.

Deliverables
ZTA: Architecture diagram mapped to NIST SP 800-207 components; before/after network reachability matrix; CISA pillar scorecard; policy repo with change logs.

Phishing: Dataset provenance sheet; training notebook; eval report with robust splits; inference service + SOC triage flow; red-team evasion results.
