# 365-ip-change

Changes happen. Across the whole IT environment. These changes sometimes need to be propagated and coordinated across different systems. One of the examples is changes made by networking teams regarding used IP address spaces, routing, public DNS, used domain names and aliases, proxies, VPN connections, firewalls, and the network stack itself. When the network team inside the organization made such changes you probably need to update something inside Microsoft 365 as an administrator to keep things working correctly.

> [!WARNING]
> Incorrect setup of these options can break things and lower user experience. Be sure about them to avoid problems.

## Internet Connection

The firewall rules, proxies, WPAD files, hosts files, routing tables, QoS settings, VPN split tunneling and similar things need to be kept updated regarding the recommendations of IP addresses, URL endpoints, and protocols used by cloud services. You can optimize the end-user experience by correct settings of these.

## Active Directory

Inside Active Directory Group Policy Objects can be references to IP addresses or websites for example in Internet Explorer Site to Zone assignments or imported favorites, location of file shares, and mapped drives. The crucial are Networks and Subnets inside Active Directory itself describing the environment, location of services and domain controllers, DNS, DHCP, and other crucial stuff. Things there can easily break whole your domain if set wrong.

## Microsoft Endpoint Configuration Manager

MECM is often tied to Active Directory and has rules for location or assignment to collections of clients based on their IP address and subnets. Bad location of Distribution Points can lead to unnecessary internet connections, delays in deployment, or worse.

## Windows 11 and Microsoft 365 Apps

Each Windows client uses internet or local probes to propagate network status to the Network Connectivity Status Indicator (NCSI). If for example VPN client breaks network status checks, some apps can refuse to connect and Outlook can stop syncing emails and show a message that the computer is offline even then you can open internet webpages.

## Microsoft 365

Microsoft 365 Admin Center is the central place for administration of tenant-wide settings and can lead you to other admin centers across all licensed services. There are a lot of links to public websites of your company like privacy links, and helpdesk websites in tenant settings which can change when the public CNAME of the domain of the company changes. Also, App Launcher can lead users to company websites outside cloud services.

- Microsoft 365 Admin Center: https://admin.microsoft.com/

### Microsoft Edge

Primary browser experience can be driven by policies set up in GPO, MDM, or Admin Center. For example, it can contain a list of locations allowed to be visited, which sites are open in IE Mode, a site list disallowed to extensions, home pages of intranet, imported favorites, and other things linked to domains.

- IE Mode: https://admin.microsoft.com/#/Edge/IEModeManagement/SiteList
- Policy Configurations: https://admin.microsoft.com/#/Edge/PolicyConfiguration

### Microsoft Search

Microsoft Search returns to Teams, SharePoint, and Bing Enterprise the location of company websites.

- Company Bookmarks: https://admin.microsoft.com/#/MicrosoftSearch/bookmarks

### Network Connectivity

Network Performance tests can lead you to a hidden need to optimize your traffic to the internet, how the services operate for users, and if problems arise, investigate which branch has a slow or unreliable connection.

- Your public egress points to the Internet: https://admin.microsoft.com/#/networkperformance

## Microsoft 365 Apps

Microsoft 365 Apps Admin Center can change the behavior of Office applications on endpoints and mobile devices and can locate corporate proxies, a list of allowed connections, or trusted locations.

- Configuration Policies: https://config.office.com/officeSettings/officePolicies

## Entra ID

Entra ID, formerly Azure AD is the single and central place of identities, cloud apps, and their security. There is located list of your internal App Registrations, endpoints of such apps, and App Galery for users which can contain URLs and hostnames. There are even App Proxy services that can publish your on-premises application to internet users. Definitely good to have these things documented.

- Entra ID Admin Center: https://entra.microsoft.com/

### Conditional Access

Policies that set company boundaries and requirements for authentication can contain known and trusted locations when MFA is not needed or where the service accounts can sign in.

- Named Locations: https://entra.microsoft.com/#view/Microsoft_AAD_ConditionalAccess/ConditionalAccessBlade/~/NamedLocations/
- Multi-Factor Authentication (Trusted IP): https://account.activedirectory.windowsazure.com/usermanagement/mfasettings.aspx

> [!TIP]
> Think twice when you add some IPv4 or IPv6 address range as known or trusted. It can lower your security posture.

## Microsoft Intune

Mobile Device Management (MDM) drives the state and configuration of your endpoints, clients, and devices across Windows, macOS, iOS, and Android. You can change the policies for VPN, Wi-Fi, Wired Networks, Internet Explorer, Intranet Sites, Site to Zone assignments, proxy locations for browsers and systems, connected file shares, and printers.

- Defender Firewall: https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/firewall
- Device Configuration Policies: https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/configuration

## Microsoft Teams

Correct settings for Skype for Business and now Microsoft Teams can improve the quality of calls and can help you investigate if problems arise even proactively by monitoring. You can report how the network behaves, how the quality of calls is inside the network, at home locations, or when connected to VPN or Wi-Fi.

- Network Topology: https://admin.teams.microsoft.com/tenantnetworksite
- Networks and Locations (Subnets, Wi-Fi, Switches, Ports): https://admin.teams.microsoft.com/networklocationmapping/subnet
- Reporting Labels: https://admin.teams.microsoft.com/reporting-labels

## Exchange Online

If you are using Exchange Online for email or even Hybrid deployment with a local Exchange Server, review your mail flow settings and connectors to make sure they are configured to accept traffic from the new IP address of your servers. Verify that your DNS records are updated to reflect the new IP address. This includes MX records for email services and any other DNS records. Maybe also your antispam rules need to be updated.

- Transport Rules: https://admin.exchange.microsoft.com/#/transportrules
- Connectors: https://admin.exchange.microsoft.com/#/connectors

> [!TIP]
> There are also other public DNS records, like Sender Policy Framework (SPF) which you probably need to check.

## SharePoint Online and OneDrive for Business

You can allow access to your intranet, sites, and user folders only from specific locations.

- Access Control: https://tenant-admin.sharepoint.com/_layouts/15/online/AdminHome.aspx#/accessControl/NetworkLocation

> [!TIP]
> Change the "tenant" for the name of your SharePoint Online instance.

## Microsoft Defender XDR

Microsoft Defender is a wide suite of services and products that secure your identities, devices, communications, data, apps, and many more. There are various security policies that can contain references to domains or IPs.

### Defender for Office 365

Antispam rules, SafeLinks do not rewrites, Tenant Allow/Block Lists, Email Authentication Settings, and Advanced Delivery change how emails come from specific IPs or domains and how they are monitored.

- Threat Policies: https://security.microsoft.com/threatpolicy

### Defender for Endpoint

Monitored Networks lead to automatic scanning of your internal network for vulnerabilities, unmanaged endpoints, and misconfigurations.

- Device Discovery: https://security.microsoft.com/securitysettings/device_discovery
- Network Assessment: https://security.microsoft.com/securitysettings/endpoints/network_assessments_assessment_jobs

### Defender for Cloud Apps

Adding known IP ranges can lower the risk for user activities.

- IP Ranges: https://security.microsoft.com/cloudapps/settings?tabid=ipRanges

### External Attack Surface Management

EASM can help protect and scan your public IP ranges, hostnames, and domains for vulnerabilities.

- Company Resources: https://security.microsoft.com/exposure-overview

> [!TIP]
> EASM has its own instance in Azure Portal for each organization with a unique name.

## Microsoft Purview

Protect your data at rest or in motion, and prevent data leakage by governance policies.

### Endpoint DLP

Specify how you protect your data on endpoints, what is company printer or share, what company domain and what is public or private, where to allow data relocation, and where not.

- DLP Settings: https://compliance.microsoft.com/datalossprevention?viewid=dlpsettings
